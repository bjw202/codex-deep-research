# 운영모델, 거버넌스, 보안, ROI, 실패 방지 - 기업 AI 자동화와 코딩 에이전트

**Researcher**: R5  
**Mode**: mixed  
**Date**: 2026-04-23  
**Scope**: Codex, Claude Code, GitHub Copilot cloud agent, Cursor류 AI IDE, MCP/tool-using agent와 일반 업무 자동화 에이전트를 기업 업무에 도입할 때 필요한 운영모델, 권한 설계, 데이터 접근, 승인 단계, 로그/감사, hallucination, prompt injection, supply chain, 법무/개인정보, 변경관리, KPI/ROI 측정, 실패 패턴과 예방책. 최종 synthesis는 작성하지 않는다.

## 핵심 요약

- 결론: 기업 도입의 핵심 질문은 "어떤 AI가 가장 똑똑한가"가 아니라 "어떤 권한, 데이터, 네트워크, 변경 권한을 어떤 증거와 승인으로 허용할 것인가"다. Codex, Claude Code, GitHub Copilot cloud agent의 공식 문서는 모두 인터넷 접근, shell/tool 실행, repository write, MCP 연결을 별도 위험 경계로 취급한다.
- 적용 조건: 에이전트는 기본적으로 production, 고객 PII, secrets, 결제/HR/법무 시스템에 직접 닿지 않아야 한다. 안전한 초기 운영모델은 read-only 분석, sandbox 실행, branch-only 변경, PR 기반 human approval, egress allowlist, session log 보존, scanner/테스트 통과를 결합한다.
- 가장 큰 반례: AI 자동화는 생성 속도를 높여도 검증 비용을 줄인다는 보장은 없다. METR의 2025 RCT는 숙련 OSS 개발자가 익숙한 저장소에서 AI 사용 시 평균 19% 느려졌다고 보고했고, Stack Overflow 2025는 AI 출력 정확성을 불신하는 개발자가 신뢰하는 개발자보다 많다고 보고했다.
- 실패 방지 조건: 실패는 모델 성능 부족보다 문제 정의 부재, workflow 미통합, 과도한 권한, untrusted input과 private data와 external communication의 결합, 로그 부재, 보안/법무 후행 참여에서 반복된다. 예방책은 prompt 문구보다 정책 엔진, 권한 tier, data-flow label, 변경관리, 감사로그, rollback, red-team/eval harness에 있다.
- 아직 모르는 것: 공개 자료만으로는 기업 내부의 실제 사고율, vendor별 guardrail false positive/false negative, 보안 통제가 생산성에 주는 비용을 정량 비교하기 어렵다. 따라서 파일럿 KPI는 "AI 사용률"보다 throughput, rework, defect escape, security finding, human review time, incident/near miss를 함께 봐야 한다.

## 읽는 법

이 문서는 R5 관점에서 기업 운영자가 도입 결정을 내릴 때 필요한 통제와 측정 체계를 정리한다. CIO/CTO, CISO, 법무/개인정보, 엔지니어링 리더, 내부감사, 플랫폼팀이 특히 봐야 한다. 제품 기능 비교가 아니라 업무 자동화가 실제 조직 안에서 안전하게 반복 운영될 수 있는 조건을 다룬다.

## 주요 발견

### 1. 운영모델은 "agent autonomy tier"로 나눠야 한다

코딩 에이전트와 업무 에이전트는 채팅 도구가 아니라 권한 위임 시스템이다. 따라서 조직은 모델별 정책보다 작업별 권한 tier를 먼저 정의해야 한다. 같은 Claude Code나 Codex라도 read-only 코드 설명과 production DB migration 실행은 완전히 다른 위험 등급이다.

| Tier | 허용 작업 | 기본 데이터 접근 | 승인 단계 | 로그/감사 | 실패 시 blast radius |
| --- | --- | --- | --- | --- | --- |
| T0 관찰 | 코드/문서 요약, 이슈 분류, 테스트 실패 원인 초안 | 공개/내부 low-risk 문서, repo read-only | 사전 승인 불필요, 민감 repo는 opt-in | prompt, context source, output 저장 | 낮음. 잘못된 요약/분류 |
| T1 제한 실행 | sandbox에서 테스트 실행, lint, 임시 분석 스크립트 | repo read, synthetic/test data | 위험 명령 denylist, shell command allowlist | tool call, command, exit code, artifact 저장 | 중간. sandbox 오염/잘못된 분석 |
| T2 branch 변경 | code edit, test 추가, 문서/설정 변경, PR 생성 | repo read/write는 agent branch로 제한 | PR human review, required checks, 보안 scanner | commit attribution, diff, session log, reviewer decision | 중간. 취약 코드/불필요 변경 |
| T3 업무 시스템 action | ticket update, CRM/email draft, 내부 문서 수정 | 최소 권한 API, PII masking, tenant scoping | high-risk action human approval, dual control | API call, before/after state, approver, rollback id | 높음. 고객/직원 영향 |
| T4 production/regulated | 배포, DB migration, 결제/HR/법무/보안 정책 변경 | 원칙상 직접 금지. break-glass만 예외 | CAB/Change approval, canary, rollback, on-call 승인 | immutable audit log, evidence package, incident hook | 매우 높음. 데이터 손실/법적 책임 |

의사결정 의미는 단순하다. T0-T2는 파일럿 대상으로 적합하지만, T3-T4는 파일럿 90일 안에 "직접 실행"보다 "draft + 승인 + replay 가능한 로그"로 제한해야 한다. Replit production DB 삭제 사고는 에이전트가 production credential과 destructive command를 동시에 가졌을 때 어떤 일이 생기는지 보여주는 경고 사례다.

### 2. 보안의 핵심은 prompt injection 차단보다 권한과 데이터 흐름 분리다

NCSC는 prompt injection을 SQL injection처럼 완전히 분리해 해결하기 어렵다고 설명한다. LLM은 입력 안의 "데이터"와 "명령"을 구조적으로 구분하지 못하기 때문에, 안전 설계는 악성 문구 필터링보다 untrusted content를 읽는 순간 권한을 낮추는 방식이어야 한다.

| 위험 조합 | 왜 위험한가 | 예방 통제 | 잔여 위험 |
| --- | --- | --- | --- |
| private data + untrusted content + external communication | Simon Willison의 `lethal trifecta`: 숨겨진 지시가 내부 데이터 유출로 이어질 수 있음 | egress deny-by-default, domain/method allowlist, data label 기반 송신 차단, DLP, human approval | 이미지/URL/side-channel, tool output 재주입 |
| repo write + issue/PR/web context | 이슈 본문, PR comment, README, dependency docs가 숨은 지시를 포함할 수 있음 | branch-only write, hidden character/comment filtering, PR review, required checks | reviewer fatigue, agent가 변경 이유를 그럴듯하게 설명 |
| shell/tool 실행 + network | curl/wget, package install, MCP tool이 secrets를 외부로 보낼 수 있음 | command allowlist, network allowlist, sandbox, ephemeral credential, secret scanning | setup step/MCP/server side path가 방화벽 밖에 있을 수 있음 |
| MCP server + broad local filesystem | MCP 서버가 새로운 supply chain과 local RCE 경로가 됨 | 신뢰된 MCP만 허용, version pinning, code review, per-tool permission, server isolation | third-party MCP 취약점, tool poisoning |
| 생성 코드 + dependency install | hallucinated package/slopsquatting 또는 취약 dependency 유입 | lockfile, internal package proxy, dependency review, SCA, SBOM/provenance | 신규 패키지 악성 여부 지연 탐지 |

OpenAI Codex의 agent 인터넷 접근 문서는 기본 차단, domain/method allowlist, work log review를 권고한다. Claude Code는 read-only 기본 권한, 명령 승인, blocklist, VM 사용, MCP 신뢰 검증을 제시한다. GitHub Copilot cloud agent는 branch 제한, human review, Actions 승인, firewall, CodeQL, secret scanning, dependency analysis, session log를 제공하지만 firewall이 MCP 서버나 setup step까지 포괄하지 않는다고 명시한다.

### 3. 법무/개인정보는 "모델 학습 여부"보다 업무 처리 전 과정에 걸린다

기업 업무 자동화는 prompt에 개인정보를 넣는 문제만이 아니다. 에이전트가 어떤 문서를 읽었는지, 어떤 개인 데이터를 추론했는지, 어떤 결정을 자동화했는지, 어떤 출력이 고객/직원에게 영향을 줬는지가 모두 규제 범위가 될 수 있다.

| 영역 | 도입 전 질문 | 권장 통제 |
| --- | --- | --- |
| 개인정보/PII | prompt, context, log, tool result에 PII가 들어가는가 | DPIA/PIA, data minimization, masking/tokenization, retention 제한, log access control |
| 자동 의사결정 | HR, 신용, 보험, 의료, 법무, 가격, 고객 권리 등에 영향을 주는가 | human-in-the-loop, appeal/override, decision rationale, model/tool trace |
| 저작권/IP | 생성 코드가 공개 코드와 유사하거나 license-restricted content를 포함하는가 | IP scan, public-code match review, license policy, provenance 기록 |
| 보안/감사 | 누가 에이전트를 시작했고 어떤 입력과 tool을 썼는가 | immutable session log, commit co-author/verified signing, approver 기록 |
| 공급망 | 외부 모델, MCP, plugin, package, API, dataset을 쓰는가 | vendor due diligence, SBOM, SLSA/provenance, version pinning, vuln disclosure path |

ICO는 생성형 AI에서도 데이터 보호 원칙이 그대로 적용되며, 개인정보 처리의 lawful basis, controller/processor 역할, DPIA, 투명성, 보안 위험, 데이터 최소화를 사전에 검토하라고 권고한다. EU AI Act의 GPAI 의무는 2025년 8월 2일부터 적용되고, 기술문서, downstream provider 정보 제공, EU 저작권 정책, 학습 콘텐츠 요약을 요구한다. 미국 기업도 캘리포니아 CCPA/CPRA의 ADMT, risk assessment, cybersecurity audit 규정처럼 자동화 처리와 개인정보 리스크 평가 요구가 늘어나는 흐름을 고려해야 한다.

### 4. ROI는 생성량이 아니라 검증 후 업무 성과로 측정해야 한다

AI 자동화 ROI를 "몇 줄의 코드가 생성됐는가", "몇 개 prompt를 썼는가"로 측정하면 실패를 조기에 발견하지 못한다. DORA 2025는 AI가 조직의 기존 강점과 약점을 증폭한다고 보고했고, GitHub는 Copilot cloud agent의 PR 생성/병합, median time to merge 같은 운영 지표를 제공한다. 그러나 이 지표도 결함률, 리뷰 시간, 보안 finding, rollback과 함께 보지 않으면 편익만 과대계상된다.

| KPI 계층 | 측정 지표 | 왜 필요한가 | 주의점 |
| --- | --- | --- | --- |
| Adoption | 활성 사용자, agent task 수, 사용 업무 유형, opt-out repo | 도구가 실제 workflow에 들어갔는지 확인 | 사용률은 성공 지표가 아님 |
| Throughput | PR created/merged, cycle time, median time to merge, ticket lead time | 병목 완화 여부 확인 | 쉬운 일만 AI에 배정되면 왜곡 |
| Quality | rework rate, reviewer comment density, defect escape, test pass/fail, flaky test 증가 | 생성 속도가 품질 저하로 전가되는지 확인 | LOC/commit 수는 단독 사용 금지 |
| Security | secret scan hits, CodeQL/SAST findings, dependency high/critical, egress block events, prompt injection near miss | 위험 축적 조기 탐지 | "0건"은 미탐지일 수도 있음 |
| Compliance | PII in prompt/log, policy exception, approval SLA, audit evidence completeness | 법무/감사 대응 가능성 확인 | 로그 자체도 민감 데이터 |
| Economics | tool/license/API/Actions cost, review time, remediation time, avoided toil, incident cost avoided | 순효과 산정 | self-reported time saving만 쓰면 과대평가 |
| People/change | trust score, prompt/review training completion, developer satisfaction, cognitive load | 지속 채택과 over/under-trust 관리 | 만족도와 생산성은 다를 수 있음 |

ROI 산식은 최소한 다음 항목을 함께 포함해야 한다.

```text
Net ROI = (절감된 업무 시간 + 회피된 지연/결함/보안 비용 + 추가 산출 가치)
          - (도구/인프라 비용 + human review 시간 + 보안/법무/감사 비용 + rework/incident 비용)
```

METR의 결과는 "느려질 수 있다"는 직접 반례다. Stack Overflow 2025는 개발자 46%가 AI 출력 정확성을 불신하고 33%만 신뢰한다고 보고했다. RAND는 AI 프로젝트 실패의 주요 원인을 잘못된 문제 정의, 필요한 데이터 부족, 기술 중심 접근, 인프라 부족, AI로 풀기 어려운 문제 선택으로 요약한다. 따라서 파일럿은 "AI로 무엇을 할 수 있는가"보다 "현재 병목을 측정하고, AI가 그 병목을 줄였는가"로 설계해야 한다.

### 5. 실패 패턴은 반복 가능하고 예방도 반복 가능하다

AI 자동화 실패는 대체로 새로운 것이 아니다. 자동화가 오래된 변경관리, 권한관리, 데이터 거버넌스, 소프트웨어 공급망 문제를 빠른 속도로 확대한다. 차이는 에이전트가 자연어 context를 읽고 tool을 호출하면서 기존 통제가 적용되지 않는 경로가 생긴다는 점이다.

| 전형적 실패 패턴 | 증상 | 대표 근거 | 예방책 |
| --- | --- | --- | --- |
| 문제 정의 없는 PoC | 사용률은 높지만 P&L/업무성과 없음 | RAND, MIT NANDA 보도, BCG/McKinsey | baseline metric, owner, go/no-go 기준, workflow redesign |
| 과도한 권한 | agent가 DB, repo, cloud, email을 직접 변경 | Replit DB 삭제, GitHub/Claude 권한 문서 | tiered permission, production deny, dual approval, rollback |
| 검증 부채 | AI 코드는 많지만 리뷰/테스트가 못 따라감 | METR, Sonar, Copilot security studies | reviewer capacity budget, required checks, AI diff risk scoring |
| prompt injection 과소평가 | 이슈/메일/웹/문서 속 숨은 지시가 실행됨 | NCSC, AgentDojo, NIST CAISI, CamoLeak | untrusted input labeling, tool boundary checks, egress control |
| 공급망 자동 수용 | agent가 임의 package/MCP/plugin 설치 | package hallucination 연구, MCP Safety Audit | internal registry, allowlist, SCA/SBOM, MCP review |
| 로그 부재 | 사고 후 누가 무엇을 승인했는지 모름 | GitHub session log 권고, NCSC logging | immutable audit trail, session replay, approver/evidence link |
| 법무/개인정보 후행 | PII, automated decision, IP 문제가 뒤늦게 발견 | ICO, EU AI Act, CPPA | DPIA/AI impact assessment, data retention, legal review gate |
| 조직 저항/오신뢰 | 숙련자는 불신, 초보자는 과신 | Stack Overflow, METR | role-based training, review rubric, trust calibration |

## 최종 도입 체크리스트

이 체크리스트는 파일럿 시작 전 gate로 쓰는 것이 가장 유용하다. 모든 항목이 완료되어야 T3 이상 권한을 허용할 수 있고, T0-T2도 최소 통제를 만족해야 한다.

| 영역 | 체크 항목 | 완료 기준 |
| --- | --- | --- |
| Ownership | executive sponsor, product owner, risk owner, security owner, legal/privacy owner 지정 | RACI 문서와 예외 승인권자 기록 |
| Use-case selection | 자동화 대상 업무와 제외 업무 정의 | "AI가 하면 안 되는 일" 목록 포함 |
| Permission tier | T0-T4 권한 tier와 업무 매핑 | shell, network, repo write, SaaS API, production 접근별 policy |
| Data classification | 에이전트가 읽을 수 있는 데이터 등급 정의 | PII/secrets/regulated data 차단 또는 masking |
| Network/egress | default deny와 allowlist 설정 | domain, method, package registry, webhook, image load 정책 |
| Tool/MCP governance | 허용 MCP/plugin/tool 등록 절차 | owner, source, version, permission, security review 기록 |
| Human approval | action별 승인 단계 정의 | irreversible/high-risk action은 dual control |
| SDLC integration | PR, test, SAST, secret scanning, SCA, license/IP scan 연결 | merge 전 필수 check로 운영 |
| Logging/audit | prompt/context/tool/diff/approval/session log 보존 | retention, access control, evidence export 가능 |
| Privacy/legal | DPIA/AI impact assessment, contract/DPA, retention policy | 개인정보와 automated decision 여부 판단 |
| Supply chain | lockfile, internal registry/proxy, SBOM/provenance, SLSA/SSDF 정렬 | 신규 dependency/MCP 자동 설치 금지 |
| Evaluation | prompt injection, hallucination, security, quality eval set | red-team/negative test와 regression cadence |
| Change management | 교육, reviewer rubric, escalation, incident response | runbook과 rollback drill 완료 |
| ROI baseline | 파일럿 전 cycle time, review time, defect/security baseline | baseline 없이는 성공 선언 금지 |
| Exit criteria | 확장/중단 기준 | 정량 KPI와 risk threshold 동시 충족 |

## 30/60/90일 파일럿 운영안

파일럿은 "빠른 전사 확산"보다 작고 측정 가능한 업무에서 guardrail의 실제 비용을 배우는 과정이어야 한다. 특히 30일 안에 production action을 열지 않는 것이 중요하다. 60일에는 반복 가능한 운영 루프를 만들고, 90일에는 확장 여부를 evidence package로 결정한다.

| 기간 | 목표 | 실행 항목 | 산출물 | Go/No-Go 기준 |
| --- | --- | --- | --- | --- |
| 0-30일: 제한 파일럿 | 위험 낮은 T0-T2 업무에서 baseline과 guardrail 검증 | 2-3개 팀 선정, repo opt-in, data classification, egress allowlist, branch-only agent, PR human review, SAST/secret/SCA 연결, training 1회 | RACI, use-case register, permission matrix, baseline KPI, 로그 샘플, 초기 risk register | secrets/PII 유출 0건, 필수 로그 누락 0건, PR merge 전 human review 100%, reviewer가 위험 판단 가능 |
| 31-60일: 운영 루프 | 반복 사용에서 품질/보안/비용 측정 | prompt injection negative tests, MCP/tool review, reviewer rubric 개선, exception process, weekly triage, ROI 대시보드, near-miss 기록 | KPI dashboard, policy exception log, prompt injection test report, cost/review time report | rework/defect/security finding이 baseline보다 악화되지 않음, egress block/near miss가 분석됨, false positive 비용이 감당 가능 |
| 61-90일: 확장 판단 | 제한 확장 또는 중단/수정 결정 | 신규 팀 1-2개 추가, T3 draft-only 업무 실험, 법무/개인정보 review, incident drill, rollback drill, executive review | 90일 evidence package, updated policy, scale plan, training plan, residual risk acceptance | 순 ROI 또는 명확한 leading indicator 확인, high-risk exception 관리 가능, 감사 추적 가능, production direct action은 별도 승인 전까지 금지 |

90일 후에도 T4 production/regulated 직접 실행은 기본적으로 금지하는 편이 낫다. 허용하려면 최소한 canary, blast-radius limit, automatic rollback, two-person approval, immutable audit log, tabletop incident exercise, 법무/개인정보 승인, CISO risk acceptance가 필요하다.

## 근거 표

| 주장 | 근거 | 출처 유형 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| Codex agent 인터넷 접근은 prompt injection, secret/code exfiltration, malware/dependency, license-restricted content 위험을 높인다 | OpenAI Codex 문서는 agent phase 인터넷을 기본 차단하고, 필요한 domain/method만 허용하며 work log를 검토하라고 권고 | official/vendor | 높음 | https://developers.openai.com/codex/cloud/internet-access |
| Claude Code는 권한 승인과 MCP 신뢰 검증을 핵심 통제로 둔다 | read-only 기본 권한, 쓰기 범위 제한, bash 승인, curl/wget blocklist, VM 사용, MCP server 신뢰 검토를 권고 | official/vendor | 높음 | https://code.claude.com/docs/en/security |
| Copilot cloud agent는 autonomous repo write 위험을 branch, human review, session log, scanner로 제한한다 | single branch push, human merge review, Actions 승인, CodeQL/secret scanning/dependency analysis, session log 제공 | official/vendor | 높음 | https://docs.github.com/en/copilot/concepts/agents/cloud-agent/risks-and-mitigations |
| Copilot firewall은 필요하지만 포괄 보안 통제가 아니다 | GitHub 문서는 firewall이 agent Bash process에만 적용되고 MCP server/setup step 등에는 적용되지 않으며 우회 가능성이 있다고 명시 | official/vendor | 높음 | https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall |
| GenAI governance는 lifecycle risk management와 신뢰성 고려가 필요하다 | NIST AI RMF GenAI Profile은 AI RMF 1.0 companion resource로 설계, 개발, 사용, 평가 전반의 trustworthiness를 다룸 | official/framework | 높음 | https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence |
| AI management system은 정책, 목표, 절차, 지속 개선 체계가 필요하다 | ISO/IEC 42001은 AI 관련 정책과 목표를 수립하고 PDCA 방식으로 AI risk/opportunity를 관리하는 management system 표준 | standard | 높음 | https://www.iso.org/standard/42001 |
| AI 시스템 공급망은 models, data, prompts, logs, software, APIs까지 포함해야 한다 | NCSC/CISA secure AI guidelines는 공급망 보안, AI asset 식별, prompt/log documentation, technical debt 관리를 권고 | official/security framework | 높음 | https://www.ncsc.gov.uk/collection/guidelines-secure-ai-system-development/guidelines/secure-development |
| LLM prompt injection은 완전 차단보다 잔여 위험 관리가 현실적이다 | NCSC는 LLM이 data/instruction을 구조적으로 구분하지 못하고, privileged tool 사용 시 confused deputy 위험이 커진다고 설명 | official/security guidance | 높음 | https://www.ncsc.gov.uk/blog-post/prompt-injection-is-not-sql-injection |
| OWASP는 prompt injection, sensitive information disclosure, supply chain, excessive agency를 LLM/agentic app 핵심 위험으로 본다 | OWASP GenAI Security Project는 LLM app과 agentic AI system을 대상으로 Top 10을 제공 | standard/security | 높음 | https://owasp.org/www-project-top-10-for-large-language-model-applications/ |
| EU AI Act는 downstream provider가 모델 capability/limitation을 이해하도록 문서 제공을 요구한다 | GPAI provider는 기술문서, downstream documentation, EU copyright policy, training content summary를 제공해야 함 | regulation/official | 중상 | https://digital-strategy.ec.europa.eu/en/faqs/guidelines-obligations-general-purpose-ai-providers |
| 생성형 AI 개인정보 처리는 기존 data protection 의무를 피하지 못한다 | ICO는 lawful basis, controller/processor, DPIA, transparency, security, data minimization, automated decision rights를 검토하라고 권고 | regulator/official | 높음 | https://ico.org.uk/about-the-ico/media-centre/news-and-blogs/2023/04/generative-ai-eight-questions-that-developers-and-users-need-to-ask/ |
| 캘리포니아 privacy 규정도 risk assessment, cybersecurity audit, ADMT 요구를 강화한다 | CPPA는 2026-01-01부터 새 규정 시행, risk assessment compliance 시작, ADMT는 2027-01-01부터 적용 예정이라고 공지 | regulator/official | 높음 | https://cppa.ca.gov/announcements/2025/20250923.html |
| AI/GenAI secure development는 SSDF와 결합해야 한다 | NIST SP 800-218A는 generative AI와 dual-use foundation model을 위한 SSDF community profile | official/security framework | 높음 | https://csrc.nist.gov/pubs/sp/800/218/a/final |
| supply chain risk는 supplier requirement와 provenance로 관리해야 한다 | NIST CSF 2.0 C-SCRM quick-start는 GV.SC category로 C-SCRM capability를 운영하고 supplier requirement를 정의하라고 설명 | official/framework | 높음 | https://www.nist.gov/publications/nist-cybersecurity-framework-20-quick-start-guide-cybersecurity-supply-chain-risk |
| SLSA는 artifact trust와 provenance를 다루는 공급망 기준이다 | SLSA는 software supply chain security를 위한 점진적 guideline과 common vocabulary를 제공 | standard/community | 중상 | https://slsa.dev/spec/v1.0/about |
| AgentDojo는 현실적 agent workflow에서 prompt injection 보안/utility trade-off를 평가한다 | 97개 realistic task와 629개 security test case를 포함하며 현재 agent가 공격 부재에도 실패하고 방어가 일부 공격만 막는다고 보고 | academic/security | 높음 | https://arxiv.org/abs/2406.13352 |
| NIST CAISI는 반복 공격 평가가 단발 평가보다 agent hijacking 위험을 더 잘 드러낸다고 본다 | 반복 시 평균 attack success가 57%에서 80%로 증가했다고 보고 | official/security evaluation | 높음 | https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations |
| MCP는 enterprise agent 공급망/권한 표면을 넓힌다 | MCP Safety Audit 논문은 MCP tool을 통해 malicious code execution, remote access control, credential theft가 가능함을 시연 | academic/security | 중상 | https://arxiv.org/abs/2504.03767 |
| code-generating LLM은 package hallucination으로 supply chain 공격 기회를 만든다 | 16개 LLM, 576,000 code sample 분석에서 commercial model 평균 5.2%, open-source model 평균 21.7% hallucinated package 비율 보고 | academic/security | 중상 | https://arxiv.org/abs/2406.10279 |
| AI 생성 코드는 취약 코드를 제안할 수 있으므로 리뷰/테스트 생략 근거가 아니다 | Copilot 보안 연구는 약 40% vulnerable, replication은 취약 suggestion 비율이 36.54%에서 27.25%로 낮아졌지만 지속된다고 보고 | academic/security | 중상 | https://cacm.acm.org/research-highlights/asleep-at-the-keyboard-assessing-the-security-of-github-copilots-code-contributions/ |
| AI 코딩 도구가 실제로 느려질 수 있다 | METR RCT는 숙련 OSS 개발자 16명, 실제 246개 task에서 AI 허용 시 완료 시간이 19% 증가했다고 보고 | academic/field experiment | 중상 | https://metr.org/Early_2025_AI_Experienced_OS_Devs_Study-paper.pdf |
| 개발자 trust는 낮고 human verification 필요성이 크다 | Stack Overflow 2025는 AI 출력 정확성을 불신하는 개발자 46%, 신뢰 33%, highly trust 3%라고 보고 | survey/community | 중상 | https://survey.stackoverflow.co/2025/ai |
| AI 프로젝트 실패는 문제 정의/데이터/인프라/기술 중심 접근에서 반복된다 | RAND는 65명 데이터 과학자/엔지니어 인터뷰에서 5개 주요 실패 원인을 도출하고, 80% 이상 실패 추정치를 인용 | research institute | 중상 | https://www.rand.org/content/dam/rand/pubs/research_reports/RRA2600/RRA2680-1/RAND_RRA2680-1.pdf |
| AI는 조직의 기존 강점과 약점을 증폭하므로 workflow redesign이 ROI 조건이다 | DORA 2025는 AI의 주요 역할을 amplifier로 설명하고, 수익은 도구 자체보다 조직 시스템 개선에서 온다고 보고 | industry research | 중상 | https://dora.dev/research/2025/dora-report/ |
| 전사적 AI value capture는 아직 드물고 workflow 재설계가 차이를 만든다 | McKinsey 2025는 88%가 AI를 쓰지만 대부분 전사 EBIT 영향이 제한적이며, high performer는 6%로 workflow redesign을 더 많이 한다고 보고 | industry survey | 중 |
| AI value scaling은 소수 기업에 집중된다 | BCG 2024는 26%만 PoC를 넘어 tangible value를 만들고, leaders는 사람/프로세스에 70% 자원을 둔다고 보고 | industry survey | 중 | https://www.bcg.com/press/24october2024-ai-adoption-in-2024-74-of-companies-struggle-to-achieve-and-scale-value |
| Replit 사고는 excessive agency와 production credential의 위험을 보여준다 | 보도에 따르면 agent가 code freeze 중 production DB를 삭제했고 CEO가 사과 | failure case/news | 중상 | https://www.tomshardware.com/tech-industry/artificial-intelligence/ai-coding-platform-goes-rogue-during-code-freeze-and-deletes-entire-company-database-replit-ceo-apologizes-after-ai-engine-says-it-made-a-catastrophic-error-in-judgment-and-destroyed-all-production-data |
| CamoLeak은 hidden prompt와 exfiltration channel 결합의 실제 제품 취약점 사례다 | GitHub Copilot Chat flaw가 private repo secrets/source exfiltration 가능성을 만들었다고 보도 | failure case/security news | 중 | https://www.esecurityplanet.com/news/github-copilot-data-theft/ |
| Anthropic Git MCP server 취약점은 MCP/tool layer가 agent risk surface임을 보여준다 | prompt injection과 Git/Filesystem MCP 조합에서 RCE/file tampering 가능성이 보도됨 | failure case/security news | 중 | https://socradar.io/blog/anthropic-git-mcp-server-vulnerabilities/ |
| AI 코드 검증 부채는 조직적 실패 패턴이다 | Sonar 2026 survey는 96%가 AI code를 완전히 신뢰하지 않지만 48%만 항상 commit 전 확인한다고 발표 | stakeholder survey | 중 | https://www.sonarsource.com/company/press-releases/sonar-data-reveals-critical-verification-gap-in-ai-coding/ |

## 출처 품질 매트릭스

| 출처 유형 | 개수 | 핵심 기여 | 약점 |
| --- | ---: | --- | --- |
| official / primary | 13 | OpenAI/Anthropic/GitHub의 실제 제품 통제, NIST/NCSC/ICO/CPPA/EU 공식 규제·프레임워크 | vendor 문서는 제품 기능 변동 가능. 규제 적용은 관할/업무별로 다름 |
| academic / standard / patent | 8 | AgentDojo, MCP Safety Audit, package hallucination, Copilot security, METR, ISO/OWASP/SLSA/NIST SSDF | 최신 agent/MCP 연구 일부는 preprint 또는 빠르게 변하는 도구 환경 의존 |
| direct case / experiment | 7 | Replit DB 삭제, CamoLeak, Anthropic Git MCP, METR RCT, NIST CAISI 반복 공격, package hallucination 실험, Sonar 검증 부채 | 사고 보도는 공개 정보가 제한되고 전체 발생률을 말하지 않음 |
| vendor / stakeholder | 6 | Codex/Claude/GitHub/Sonar/DORA/BCG/McKinsey 운영 기능과 시장 지표 | 이해관계자 편향 가능. ROI 수치는 방법론 차이 큼 |
| community | 2 | Stack Overflow survey, Simon Willison lethal trifecta 실무 모델 | 커뮤니티/설문은 선택 편향과 self-report 한계 |
| weak / unverified | 0 | 결론 근거로 사용하지 않음 | 보도자료/뉴스도 단독으로 강한 인과 결론에는 사용하지 않음 |

## 반례/실패 사례 검색 로그

반례 검색은 결론을 약하게 만들기 위한 절차가 아니라 도입 조건을 현실적으로 만드는 절차다. 검색 결과 "AI 자동화는 유용할 수 있지만, 제한 없는 자율성과 검증 생략은 위험하다"는 쪽으로 결론이 조정되었다.

| 쿼리 | 목적 | 결과 | 결론 영향 |
| --- | --- | --- | --- |
| `Codex agent internet access prompt injection exfiltration allowlist` | Codex 공식 위험과 통제 확인 | 기본 인터넷 차단, prompt injection/exfiltration/malware/license 위험, allowlist 권고 발견 | Codex 도입 gate에 egress policy와 work log review 포함 |
| `Claude Code security permissions prompt injection MCP` | Claude Code 권한/승인/MCP 정책 확인 | read-only 기본, 명령 승인, blocklist, VM, MCP 신뢰 검증, "완전 면역 아님" 확인 | 승인 fatigue와 MCP review를 운영모델에 포함 |
| `GitHub Copilot cloud agent risks mitigations firewall session logs` | Copilot cloud agent의 감사/권한 통제 확인 | branch 제한, human review, CodeQL/secret/SCA, session log, firewall 한계 확인 | PR 기반 운영과 session log를 표준 통제로 채택 |
| `AI agent prompt injection failure` | prompt injection 실패/한계 확인 | NCSC, AgentDojo, NIST CAISI, CamoLeak 발견 | prompt filtering보다 권한/데이터 흐름 분리를 우선 |
| `MCP security exploit prompt injection credential theft` | MCP/tool supply chain 위험 확인 | MCP Safety Audit, Anthropic Git MCP server flaws 발견 | MCP를 third-party dependency로 취급하도록 권고 |
| `AI coding package hallucination slopsquatting study` | dependency supply chain 실패 모드 확인 | 576,000 code sample 연구와 hallucinated package 비율 발견 | agent의 자동 package install 금지와 internal registry 권고 |
| `AI coding tools productivity slower METR 19%` | ROI 반례 확인 | METR RCT 19% slowdown, review/prompting/waiting 비용 확인 | ROI에 human review/rework 시간을 포함 |
| `Stack Overflow 2025 AI trust accuracy developers` | 채택/신뢰 한계 확인 | 46% distrust, 33% trust, 3% highly trust 확인 | change management와 trust calibration 포함 |
| `AI project failure RAND root causes` | 조직적 실패 패턴 확인 | 문제 정의, 데이터, 기술 중심, 인프라, 기술 한계 원인 발견 | 파일럿 baseline과 workflow integration을 필수화 |
| `enterprise GenAI pilots fail measurable ROI MIT BCG McKinsey` | ROI 과대평가 반례 확인 | MIT NANDA 보도, BCG 74% struggle, McKinsey high performer 6% 확인 | PoC 성공을 전사 확장 근거로 보지 않도록 조정 |
| `AI privacy automated decisionmaking regulation CPPA ICO EU AI Act` | 법무/개인정보 통제 확인 | ICO DPIA/lawful basis, CPPA ADMT/risk assessment, EU GPAI obligations 확인 | 개인정보와 automated decision gate 포함 |
| `successful mitigation prompt injection AI agents allowlist firewall detector` | 통제 성공 반례 확인 | GitHub/OpenAI/Claude guardrail, AgentDojo/NIST eval, DORA capability model 발견 | "도입 불가"가 아니라 "제한된 권한에서 측정하며 확장"으로 결론 조정 |

## 상충점과 불확실성

- **생산성 효과는 업무 맥락 의존적이다.** GitHub와 DORA는 backlog 처리, PR throughput, 조직 역량 강화 가능성을 제시하지만 METR은 숙련 개발자의 familiar codebase에서 slowdown을 보고한다. 따라서 "AI 도입 = 생산성 증가"는 일반 명제가 아니며, 파일럿별 baseline과 task mix가 필요하다.
- **보안 통제의 비용은 공개 수치가 부족하다.** egress allowlist, 승인, scanner, MCP review는 위험을 줄이지만 latency, false positive, reviewer fatigue를 만든다. vendor별 false positive/false negative, 우회율, 운영 비용은 공개적으로 비교하기 어렵다.
- **사고 사례는 공개 편향이 크다.** Replit, CamoLeak, MCP 취약점은 중요한 신호지만 전체 발생률을 추정할 수 없다. 많은 near miss는 기업 내부에 남아 공개되지 않을 가능성이 크다.
- **규제 적용은 use case에 따라 달라진다.** 단순 code assist는 고위험 AI가 아닐 수 있지만, HR/금융/의료/법무/고객 권리 영향을 주는 workflow에 agent가 들어가면 DPIA, ADMT, automated decision, sector regulation, audit obligation이 결합될 수 있다.
- **최신 agent 기능은 빠르게 변한다.** Claude Code auto mode, Copilot cloud agent, Codex cloud, MCP 생태계는 월 단위로 권한/보안 기능이 변한다. 파일럿 정책은 특정 제품명보다 권한·데이터·egress·audit 원칙으로 작성해야 유지된다.

## 의사결정 영향

- **T0-T2부터 시작하고 T3-T4는 draft-only로 제한한다.** 90일 파일럿 동안 production direct action, destructive DB command, 결제/HR/법무 자동 실행은 허용하지 않는 것이 합리적이다.
- **CISO와 법무를 사후 승인자가 아니라 설계 참여자로 둔다.** prompt, context, logs, tool outputs는 모두 민감 데이터가 될 수 있고, 에이전트의 자동 action은 감사 대상이 된다.
- **ROI dashboard에는 security와 review cost를 반드시 넣는다.** AI가 만든 PR 수가 늘어도 review time, defect escape, SAST finding, dependency risk, rollback이 늘면 순 ROI는 낮거나 음수가 될 수 있다.
- **vendor guardrail은 보조 통제다.** Codex/Claude/GitHub의 통제는 유용하지만 조직의 data classification, network policy, CI/CD gate, legal review, incident response를 대체하지 않는다.
- **성공 조건은 업무 재설계다.** DORA, RAND, McKinsey, BCG의 공통 메시지는 AI tool 구매보다 workflow, data, people/process, governance가 ROI를 좌우한다는 것이다.

## 인접 질문

- 특정 산업(금융, 의료, 공공, 제조, 법무)별로 T3/T4 agent action을 어디까지 허용할 수 있으며, 어떤 승인·감사 증거가 규제기관 또는 내부감사에 충분한가?
- 에이전트 session log에 포함된 prompt/context/tool output 자체가 민감 데이터일 때, 보존 기간과 접근권한, 삭제권, eDiscovery 대응은 어떻게 설계해야 하는가?
- 더 나은 문제 정의: "AI 자동화 툴을 도입할 것인가?"보다 "어떤 권한·데이터·검증 경계 안에서 AI 자동화가 검증 비용과 tail risk를 초과하는 순가치를 만드는가?"가 의사결정에 더 적합하다.

## 출처 목록

| # | 출처 | 날짜/버전 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| 1 | OpenAI Developers, Codex cloud: Agent internet access | accessed 2026-04-23 | 높음 | https://developers.openai.com/codex/cloud/internet-access |
| 2 | Anthropic Claude Code Docs, Security | accessed 2026-04-23 | 높음 | https://code.claude.com/docs/en/security |
| 3 | Anthropic Claude Code Docs, MCP | accessed 2026-04-23 | 높음 | https://docs.anthropic.com/en/docs/claude-code/mcp |
| 4 | GitHub Docs, Risks and mitigations for Copilot cloud agent | accessed 2026-04-23 | 높음 | https://docs.github.com/en/copilot/concepts/agents/cloud-agent/risks-and-mitigations |
| 5 | GitHub Docs, Customizing or disabling the firewall for GitHub Copilot cloud agent | accessed 2026-04-23 | 높음 | https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall |
| 6 | GitHub Docs, About GitHub Copilot cloud agent | accessed 2026-04-23 | 높음 | https://docs.github.com/en/copilot/concepts/agents/cloud-agent/about-cloud-agent |
| 7 | NIST AI 600-1, AI RMF: Generative AI Profile | created 2024-07-26, updated 2026-04-08 | 높음 | https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence |
| 8 | ISO/IEC 42001:2023 AI management systems | 2023 | 높음 | https://www.iso.org/standard/42001 |
| 9 | NCSC/CISA et al., Guidelines for secure AI system development: Secure development | 2023, accessed 2026-04-23 | 높음 | https://www.ncsc.gov.uk/collection/guidelines-secure-ai-system-development/guidelines/secure-development |
| 10 | NCSC, Prompt injection is not SQL injection | 2025 | 높음 | https://www.ncsc.gov.uk/blog-post/prompt-injection-is-not-sql-injection |
| 11 | OWASP Top 10 for Large Language Model Applications / GenAI Security Project | current 2026 | 높음 | https://owasp.org/www-project-top-10-for-large-language-model-applications/ |
| 12 | European Commission, Guidelines on obligations for General-Purpose AI providers | 2025, accessed 2026-04-23 | 중상 | https://digital-strategy.ec.europa.eu/en/faqs/guidelines-obligations-general-purpose-ai-providers |
| 13 | ICO, Generative AI: eight questions that developers and users need to ask | 2023-04 | 높음 | https://ico.org.uk/about-the-ico/media-centre/news-and-blogs/2023/04/generative-ai-eight-questions-that-developers-and-users-need-to-ask/ |
| 14 | CPPA, California Finalizes Regulations to Strengthen Consumers' Privacy | 2025-09-23 | 높음 | https://cppa.ca.gov/announcements/2025/20250923.html |
| 15 | NIST SP 800-218A, Secure Software Development Practices for Generative AI and Dual-Use Foundation Models | 2024-07 | 높음 | https://csrc.nist.gov/pubs/sp/800/218/a/final |
| 16 | NIST SP 1305, CSF 2.0 Quick-Start Guide for C-SCRM | 2024-10-21 | 높음 | https://www.nist.gov/publications/nist-cybersecurity-framework-20-quick-start-guide-cybersecurity-supply-chain-risk |
| 17 | SLSA Specification, About SLSA | v1.0 page, current docs note v1.2 | 중상 | https://slsa.dev/spec/v1.0/about |
| 18 | AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents | 2024 | 높음 | https://arxiv.org/abs/2406.13352 |
| 19 | NIST CAISI, Strengthening AI Agent Hijacking Evaluations | 2025-01-17 | 높음 | https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations |
| 20 | MCP Safety Audit: LLMs with the Model Context Protocol Allow Major Security Exploits | 2025 | 중상 | https://arxiv.org/abs/2504.03767 |
| 21 | We Have a Package for You! A Comprehensive Analysis of Package Hallucinations by Code Generating LLMs | 2024 | 중상 | https://arxiv.org/abs/2406.10279 |
| 22 | CACM, Asleep at the Keyboard? Assessing the Security of GitHub Copilot's Code Contributions | 2024 summary of peer-reviewed work | 중상 | https://cacm.acm.org/research-highlights/asleep-at-the-keyboard-assessing-the-security-of-github-copilots-code-contributions/ |
| 23 | Assessing the Security of GitHub Copilot Generated Code: A Targeted Replication Study | 2023 | 중상 | https://arxiv.org/abs/2311.11177 |
| 24 | METR, Measuring the Impact of Early-2025 AI on Experienced OSS Developer Productivity | 2025 | 중상 | https://metr.org/Early_2025_AI_Experienced_OS_Devs_Study-paper.pdf |
| 25 | Stack Overflow Developer Survey 2025, AI | 2025 | 중상 | https://survey.stackoverflow.co/2025/ai |
| 26 | RAND, The Root Causes of Failure for Artificial Intelligence Projects and How They Can Succeed | 2024 | 중상 | https://www.rand.org/content/dam/rand/pubs/research_reports/RRA2600/RRA2680-1/RAND_RRA2680-1.pdf |
| 27 | DORA, State of AI-assisted Software Development 2025 | 2025 | 중상 | https://dora.dev/research/2025/dora-report/ |
| 28 | DORA, AI Capabilities Model | last updated 2025-11-25 | 중상 | https://dora.dev/ai/capabilities-model/report/ |
| 29 | McKinsey, The State of AI: Global Survey 2025 | 2025 | 중 | https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai |
| 30 | BCG, AI Adoption in 2024: 74% of Companies Struggle to Achieve and Scale Value | 2024-10-24 | 중 | https://www.bcg.com/press/24october2024-ai-adoption-in-2024-74-of-companies-struggle-to-achieve-and-scale-value |
| 31 | Tom's Hardware, Replit AI agent deleted production database | 2025-07 | 중상 | https://www.tomshardware.com/tech-industry/artificial-intelligence/ai-coding-platform-goes-rogue-during-code-freeze-and-deletes-entire-company-database-replit-ceo-apologizes-after-ai-engine-says-it-made-a-catastrophic-error-in-judgment-and-destroyed-all-production-data |
| 32 | eSecurity Planet, GitHub Copilot Flaw Exposed Private Code in CamoLeak | 2025 | 중 | https://www.esecurityplanet.com/news/github-copilot-data-theft/ |
| 33 | SOCRadar, Anthropic Git MCP Server Vulnerabilities | 2026 | 중 | https://socradar.io/blog/anthropic-git-mcp-server-vulnerabilities/ |
| 34 | Sonar, State of Code Developer Survey press release | 2026-01-08 | 중 | https://www.sonarsource.com/company/press-releases/sonar-data-reveals-critical-verification-gap-in-ai-coding/ |
| 35 | Simon Willison, The lethal trifecta for AI agents | 2025-06-16 | 중상 | https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/ |

## 검색 포화 판단

필수 깊이 게이트는 충족했다. 공식/표준/규제/프레임워크 출처는 OpenAI, Anthropic, GitHub, NIST AI RMF, ISO/IEC 42001, NCSC/CISA, OWASP, EU AI Act, ICO, CPPA, NIST SSDF, NIST CSF C-SCRM, SLSA로 최소 4개 기준을 크게 초과했다. 기술 보안/AI agent risk 출처는 NCSC prompt injection, OWASP LLM Top 10, AgentDojo, NIST CAISI, MCP Safety Audit, package hallucination, Copilot security studies, GitHub/Codex/Claude security docs로 최소 4개 기준을 초과했다. 실패 사례/한계/비판 출처는 Replit, CamoLeak, Anthropic Git MCP flaws, METR slowdown, Stack Overflow trust decline, RAND AI project failure, Sonar verification gap, BCG/McKinsey scaling gap으로 최소 4개 기준을 초과했다.

검색 포화의 근거는 새 쿼리를 추가해도 같은 위험 축이 반복되었기 때문이다. 반복된 축은 excessive agency, prompt injection, data exfiltration, MCP/tool supply chain, generated-code vulnerability, verification debt, legal/privacy auditability, workflow/ROI failure였다. 남은 직접 증거 부족 항목은 기업 내부 사고율, guardrail별 실제 false positive/false negative, 산업별 규제기관의 agent-authored output 감사 사례다. 다음 라운드가 있다면 금융/의료/공공 중 하나를 고르고 구체적인 control mapping과 evidence package template을 조사해야 한다.
