# 리서치 저널 - AI 자동화와 코딩 에이전트 업무 워크플로우

**Date**: 2026-04-23  
**Workspace**: docs/research/2026-04-23-ai-automation-coding-agent-workflows/

## 1. 리서치 설계

이 저널은 Critic 전 Pass 1 산출물이다. 새 검색은 하지 않았고, 지정된 5개 Researcher 산출물만 읽었다. 여기서는 최종 진실 판단을 하지 않고, 각 Researcher의 주장, 수치, 출처 품질, 약한 증거 구간, 상충 후보를 Critic이 검토하기 쉬운 형태로 압축한다.

| Researcher | assignment | 주요 산출물 성격 | Journal 사용 방식 |
| --- | --- | --- | --- |
| R1 | 공개 실제 사례와 정량 효과 | n8n, Zapier, Make, Microsoft, GitHub, OpenAI, Anthropic 사례와 반례 | 실제 효과 수치와 vendor-only 편향을 분리 |
| R2 | 프런티어 랩 에이전트 방향 | OpenAI, Anthropic, Google의 제품 방향, 내부 사용, 보안 기본값, 벤치마크 | 제품 방향과 운영 경계의 수렴/차이를 정리 |
| R3 | 워크플로우 아키텍처 패턴 | n8n, Zapier, Make, LangGraph, MCP, GitHub Actions 결합 구조 | 구현 패턴, 승인 게이트, 실패 모드 추출 |
| R4 | 직무별 고가치 use case ideation | 공통, 개발/IT, 산업운영, 경영지원, 법무, 구매 후보 18개 | 최종 유즈케이스 후보와 근거 강도 분리 |
| R5 | 운영모델, 거버넌스, 보안, ROI | 권한 tier, 보안, 법무/개인정보, KPI, 30/60/90일 파일럿 | 도입 조건, 통제, ROI 측정 한계 정리 |

## 2. 한 페이지 브리핑

- 결론 후보: 다섯 산출물은 모두 `AI가 직접 끝낸다`보다 `AI가 초안, 패치, 리포트, 승인 패킷, 테스트 로그를 만들고 사람이 승인한다`는 운영 모델로 수렴한다.
- 적용 가능성이 높은 영역: 개발/IT의 issue-to-PR, CI 실패 요약, 테스트/문서 보강, 보안/운영 triage가 가장 직접 근거가 강하다. 구매, 법무, 재무, 산업운영은 가치가 크지만 승인 비용과 실패 비용도 크다.
- 가장 큰 상충: 벤더 고객사례와 공식 발표는 큰 시간 절감과 확장을 말하지만, METR, 보안 연구, RPA/AI 프로젝트 실패 연구는 검증 비용, task mismatch, 권한 사고, ROI 미실현을 반복 경고한다.
- 가장 약한 증거 구간: no-code/low-code 자동화와 코딩 에이전트를 결합한 장기 운영 데이터, 벤더 ROI 수치의 독립 감사, Codex/Claude Code/Gemini 계열의 동일 조건 head-to-head 비교가 부족하다.
- 다음 액션: Critic은 효과 수치의 독립성, 제품별 비교 일반화 가능성, 고위험 업무의 통제 충분성, use case 우선순위의 근거 강도를 우선 검토해야 한다.

## 3. Researcher 요약

### R1 - 공개 실제 사례와 정량 효과

반복 데이터 이동, 분류, 요약, 초안, 승인 흐름에서 공개 정량 사례가 많다.  
n8n, Microsoft, Zapier, Make 사례는 시간 절감 수치가 구체적이지만 대체로 vendor-only라 평균 ROI 근거로 쓰기 어렵다.  
METR의 19% slowdown과 RPA 실패 검색은 업무 선택, 검증 비용, 유지보수 비용을 반드시 반영해야 함을 보여준다.

### R2 - 프런티어 랩 에이전트 방향

OpenAI, Anthropic, Google 모두 채팅 보조에서 파일, 터미널, 브라우저, 앱, MCP, 승인 게이트를 쓰는 감독형 에이전트로 이동했다.  
공식 문서는 공통적으로 sandbox, read-only 기본값, 명령 승인, 네트워크 제한, admin control, audit를 강조한다.  
세 제품군을 같은 조건에서 직접 비교한 독립 근거는 약하므로, 공개 벤치마크 순위보다 내부 task-stratified benchmark가 필요하다.

### R3 - 워크플로우 아키텍처 패턴

안정적인 구조는 `Event -> Context -> Branch -> Agent Work -> Verification -> Approval -> Deploy/Publish -> Audit` 파이프라인으로 요약된다.  
n8n/Zapier/Make는 이벤트와 앱 연결, LangGraph는 장기 상태와 human-in-the-loop, GitHub Actions는 검증/배포 신뢰 경계, MCP는 도구 연결 표준으로 배치된다.  
약한 부분은 결합 워크플로우의 장기 실패율, 유지보수 비용, 권한 사고율에 대한 독립 실증이다.

### R4 - 직무별 고가치 유즈케이스

고가치 후보는 산출물과 승인점이 명확한 업무에 몰린다. Top 후보는 issue-to-PR, SecOps triage, supplier onboarding, contract redline, finance close/reconciliation이다.  
법무, 구매, 산업운영은 효과 여지가 크지만 hallucination, supplier data quality, 물리 안전, fraud, privilege risk 때문에 decision support로 제한해야 한다.  
후보별 근거는 충분히 넓지만, 구매/법무/재무에 Codex/Claude Code를 장기간 적용한 독립 기업 성과 데이터는 부족하다.

### R5 - 운영모델, 거버넌스, 보안, ROI

기업 도입의 핵심은 모델 성능이 아니라 권한, 데이터, 네트워크, 변경 권한을 어떤 증거와 승인으로 허용할지다.  
권장 운영은 T0 관찰, T1 제한 실행, T2 branch 변경부터 시작하고, T3 업무 시스템 action과 T4 production/regulated action은 draft-only 또는 별도 승인으로 제한하는 방식이다.  
ROI는 사용량이나 생성량이 아니라 throughput, review time, rework, defect escape, security finding, near miss, 비용까지 함께 봐야 한다.

## 4. 핵심 주장과 수치

아래 표는 최종 결론이 아니라 Critic이 검토할 핵심 주장 목록이다. 수치는 측정 조건과 출처 성격이 서로 다르므로 직접 합산하거나 순위화하면 안 된다.

| 주장 | Researcher | 확신도 | 메모 |
| --- | --- | --- | --- |
| 반복 업무 자동화는 명확한 입력/출력과 승인 흐름이 있을 때 시간 절감 사례가 많다. | R1 | 중간 | 사례 수는 많지만 다수가 vendor-only다. 업무 패턴 근거로는 강하고 평균 ROI 근거로는 약하다. |
| Vodafone/n8n은 33개 워크플로우, 5,000+ person-days 절감, £2.2M 비용 회피, 월 약 £300k 지속 절감을 주장한다. | R1 | 중간 | 구체 수치이나 n8n 고객사례다. 독립 감사 여부 불명. |
| Delivery Hero/n8n은 계정 잠금 복구에서 월 800건, 35분->20분, 월 200시간 절감을 주장한다. | R1 | 중간 | ITSM 병목 사례로 유용하나 vendor-only. |
| Stepstone/n8n은 통합 스프린트 2주->2시간, 25배 속도, 200+ 워크플로우를 주장한다. | R1 | 중간 | 데이터 통합 패턴 근거. 효과 크기는 독립 확인 필요. |
| Field Aerospace/n8n은 제안서 80% 초안을 2주/3-4명->25분으로 줄였다고 주장한다. | R1 | 중간 | 문서 긴 업무+사람 검토 패턴 근거. 수치 과대 가능성 검토 필요. |
| Microsoft Games Global은 연 22,370시간 절감, Cineplex는 환불 5-15분->1분 미만, Dunaway는 조사 시간 90% 감소를 주장한다. | R1 | 중간 | Power Platform/Copilot Studio 고객사례. 시민개발 포트폴리오 근거로 사용 가능. |
| GitHub-Accenture RCT는 PR/개발자 8.69% 증가와 제안 수락 약 30%를 보고했다. | R1 | 중상 | stakeholder 연구지만 telemetry/RCT 성격. 조건 확인 필요. |
| METR 2025 RCT는 숙련 OSS 개발자가 익숙한 코드베이스에서 AI 사용 시 19% 느려졌다고 보고했다. | R1/R5 | 높음 | 긍정 사례에 대한 핵심 반례. task mix와 숙련도 조건을 분리해야 한다. |
| OpenAI, Anthropic, Google은 모두 agent workspace, tool use, approval, sandbox 방향으로 수렴한다. | R2 | 높음 | 기능 존재와 공식 방향은 강한 official 근거. 효과 크기는 별도 문제. |
| Anthropic 내부 공개는 완전 위임 가능한 업무를 0-20%로 보고하고 감독/검증 필요성을 강조한다. | R2 | 중상 | vendor official이지만 한계까지 공개했다는 점에서 운영 모델 근거로 중요. |
| APEX-Agents 계열 업무 벤치마크는 long-horizon cross-application task의 최고 Pass@1도 24% 수준이라고 보고한다. | R2 | 중상 | 제품별 harness 비교는 아니지만 완전자율 기대치를 낮추는 근거. |
| 표준 구현 패턴은 event/context/branch/agent/verification/approval/deploy/audit로 수렴한다. | R3 | 높음 | 다수 공식 문서와 템플릿에서 구조가 반복된다. |
| MCP와 tool-using agent는 prompt injection, tool poisoning, 권한 과다 부여의 표면을 넓힌다. | R3/R5 | 높음 | MCP spec, OWASP/NIST/NCSC, 학술 보안 연구가 반복 지지. |
| Top 10 유즈케이스 중 D1 issue-to-PR와 D3 SecOps triage는 근거와 검증 경계가 가장 분명하다. | R4 | 중상 | repo/CI/PR 또는 보안 triage 산출물이 남는다. 실제 조직 baseline은 필요. |
| 법무 AI는 fake citation 및 hallucination 반례 때문에 citation verification과 변호사 승인이 필수다. | R4/R5 | 높음 | Stanford HAI, AP/ABA sanction 사례가 직접 반례를 제공. |
| ROI는 사용량이 아니라 순효과로 봐야 하며 review/rework/security/legal/audit 비용을 차감해야 한다. | R5 | 높음 | METR, RAND, DORA, BCG/McKinsey, Stack Overflow가 보정 근거. |
| R5의 30/60/90일 파일럿은 T0-T2 제한 파일럿에서 시작하고 T3는 draft-only, T4 직접 실행은 금지에 가깝게 둔다. | R5 | 중상 | 규정이 아니라 운영 권고. Critic이 적용 가능성과 과잉 보수성을 검토할 필요. |

## 5. 출처 품질 매트릭스

출처 품질은 리서치 전체의 결론 강도를 결정한다. 공식 문서와 표준은 기능/통제 존재를 강하게 뒷받침하지만, 효과 수치와 ROI는 벤더·고객 발표에 많이 의존한다.

| Researcher | official/primary | academic/standard/patent | direct case/experiment | vendor/stakeholder | weak/unverified | 비고 |
| --- | ---: | ---: | ---: | ---: | ---: | --- |
| R1 | 14 | 4 | 16+ | 14 | 다수 배제 | 실제 사례가 풍부하나 정량 효과의 독립 감사가 약하다. |
| R2 | 17 | 4 | 4 | 다수 포함 | 0 | 제품 방향과 보안 기본값은 강하고, 제품 간 직접 비교는 약하다. |
| R3 | 16 | 9 | 8 | 8 | 2 | 구현 패턴과 보안 통제는 강하나 장기 운영 데이터는 부족하다. |
| R4 | 8 | 9 | 7 | 6 | 2 | use case 폭은 넓고 통제 근거도 있으나 일부 직무 성과는 인접 근거다. |
| R5 | 13 | 8 | 7 | 6 | 0 | 거버넌스·보안·규제 근거가 강하다. 실제 사고율과 통제 비용 비교는 약하다. |
| 통합 관찰 | 68 | 34 | 42+ | 40+ | 낮은 근거는 대체로 보조만 사용 | 수량 기준으로는 충분하지만, ROI와 장기 운영 실패율에는 질적 gap이 남는다. |

## 6. 약한 증거 구간

아래 항목은 최종 synthesis에서 강한 단정으로 쓰면 위험한 구간이다. Critic은 이 구간을 `보류`, `내부 실험 필요`, `조건부 권고` 중 어디에 둘지 판단해야 한다.

| 항목 | 약한 이유 | 필요한 추가 조사 |
| --- | --- | --- |
| 벤더 고객사례의 ROI와 시간 절감률 | R1의 큰 수치 대부분이 n8n, Microsoft, Zapier, Make, OpenAI, Anthropic 고객사례다. 실패한 파일럿과 유지보수 비용이 공개되지 않을 가능성이 크다. | 독립 감사 사례, 원자료 telemetry, 도입 전후 baseline, review/rework 비용 포함 ROI. |
| no-code/low-code 자동화 + 코딩 에이전트 결합의 장기 운영 효과 | R3는 구조와 템플릿을 잘 제시했지만 장기 실패율, 권한 사고율, 유지보수 비용의 공개 실증이 부족하다고 명시했다. | 6-12개월 workflow run 로그, 실패 사유, ownership 변경 후 유지율, incident/near miss. |
| Codex, Claude Code, Gemini Code Assist/Antigravity/Jules의 동일 조건 비교 | R2는 제품별 공식 벤치마크와 일부 PR acceptance 연구를 찾았지만 세 제품군 전체의 head-to-head 직접 근거는 부족하다. | 동일 repo, 동일 task, 동일 권한, 동일 비용 조건의 내부 benchmark. |
| Google 내부 2025-2026 agent workflow 사례 | R2는 Google의 플랫폼 방향은 강하지만 최신 내부 사용 공개가 OpenAI/Anthropic보다 약하다고 적었다. | Google 내부 개발/업무 agent 운영 사례, 최신 DORA/Gemini Enterprise 세부 telemetry. |
| 구매/법무/재무에 Codex/Claude Code를 장기 적용한 독립 성과 | R4는 use case 후보를 설계했지만 구매, 법무, 재무는 인접 근거와 통제 근거가 많고 직접 장기 사례는 제한적이다. | 특정 기업의 CLM, supplier onboarding, close/reconciliation agent 운영 데이터. |
| 보안 guardrail의 비용과 false positive/false negative | R5는 egress allowlist, 승인, scanner, MCP review가 필요하다고 보지만 통제 비용의 공개 비교가 부족하다고 했다. | vendor별 guardrail 우회율, 승인 latency, reviewer fatigue, blocked false positive 비용. |
| 사고 사례의 발생률 | Replit, CamoLeak, MCP 취약점 등은 중요한 신호이나 공개 편향이 크고 전체 발생률을 말하지 않는다. | 내부 near miss 공유, 사고 taxonomy, 보험/감사/보안 벤치마크 데이터. |
| 일반 업무 자동화의 완전완료율 | APEX 계열 benchmark와 Anthropic 내부 0-20% 위임 신호는 완전자율에 부정적이지만 업무별 조건 차이가 크다. | 업무별 pass/fail 기준을 둔 사내 eval, HITL 전후 completion rate. |
| 커뮤니티 기반 실패 신호 | R1/R3/R4 일부 커뮤니티 자료는 현장 감각을 주지만 익명·비대표성 문제가 있다. | 공식 incident report, postmortem, customer interview, support ticket pattern. |

## 7. 예비 상충점

이 표는 모순을 확정하지 않는다. 같은 주장이 서로 다른 조건에서 모두 맞을 수 있으므로, Critic은 조건 차이와 일반화 가능성을 확인해야 한다.

| 항목 | A | B | 상충 유형 | Critic focus |
| --- | --- | --- | --- | --- |
| AI 코딩 생산성 | GitHub-Accenture는 PR 증가와 만족도 증가를 보고한다. | METR는 숙련 OSS 개발자가 익숙한 코드베이스에서 19% 느려졌다고 보고한다. | 조건 차이 | task type, 숙련도, 코드베이스 친숙도, 측정 지표가 다른지 검토. |
| 워크플로 자동화 ROI | R1 고객사례는 수천 시간, 수백만 비용 회피, 25배 속도를 주장한다. | R5는 review/rework/security/legal/audit 비용을 차감해야 순 ROI가 보인다고 경고한다. | 측정 범위 차이 | ROI 산식에 검증 비용과 유지보수 비용이 포함됐는지 확인. |
| 프런티어 랩 제품 방향 | R2는 agent workspace와 computer/browser/tool use 확장을 강하게 확인한다. | R2/R5는 완전 자율 성공률과 보안 기본값이 아직 제한적이라고 본다. | 기능 존재 vs 운영 가능성 | 기능 발표와 production-ready 운영 근거를 분리. |
| no-code agent 템플릿 | R3는 n8n/Zapier/Make/LangGraph 템플릿에서 반복 패턴을 추출한다. | R3는 템플릿이 보안, idempotency, rollback까지 갖춘 생산 등급인지는 별도 검토가 필요하다고 한다. | 레퍼런스 구현 강도 | 템플릿을 설계 힌트로 쓸지 production pattern으로 쓸지 구분. |
| 법무/구매/재무 자동화 | R4는 고가치 후보로 계약 redline, supplier onboarding, close/reconciliation을 제시한다. | R4/R5는 hallucination, data quality, fraud, 개인정보, 감사 리스크 때문에 자동 판단은 위험하다고 한다. | 가치 vs 실패 비용 | decision support와 final decision automation을 명확히 분리. |
| 보안 통제 | R5는 강한 guardrail과 T0-T2 제한 파일럿을 권고한다. | 과도한 승인과 allowlist는 속도와 adoption을 떨어뜨릴 수 있다. | 위험 감소 vs 운영 비용 | 최소 통제 기준과 업무별 완화 가능한 통제를 나눌 것. |
| 벤더 벤치마크 | R2는 각 벤더가 최신 벤치마크와 기능을 공개했다고 정리한다. | R2는 벤치마크 단위가 달라 순위화하면 안 된다고 경고한다. | 비교 가능성 | benchmark-to-decision mapping이 타당한지 검토. |
| MCP 확산 | R2/R3는 MCP가 company context와 tool integration의 핵심 표면이라고 본다. | R3/R5는 MCP가 tool poisoning, RCE, credential theft, 권한 과다의 표면도 넓힌다고 본다. | 표준화 편익 vs 공급망 위험 | MCP registry, permission, isolation, audit 요구 수준 검토. |

## 8. Critic / Repair / Expansion 상태

현재는 Pass 1 상태다. Critic, Verifier, Repair, Expansion은 아직 수행되지 않았다.

| 항목 | 상태 | 메모 |
| --- | --- | --- |
| Critic findings | 미수행 | 이 저널의 Critic focus를 기반으로 검토 필요. |
| External Deep Research Gate | 미검토 | Pass 1에서는 판단하지 않음. |
| Repair Queue | 없음 | Critic 이후 결함이 확정되면 생성. |
| Expansion Queue | 후보 있음 | 장기 운영 데이터, 독립 ROI, head-to-head benchmark가 후보. |
| Verifier corrections | 없음 | Critic이 특정 주장 대조를 요구할 때 수행. |
| Negative Search 수행 여부 | 수행됨 | 5개 Researcher 모두 반례/실패/한계 검색 로그를 포함. |

### Negative Search 요약

반례 검색은 단순히 결론을 약화시키기보다 도입 조건을 조정하는 역할을 했다. 반복된 실패 축은 생산성 둔화, RPA/AI 프로젝트 실패, prompt injection, MCP/tool poisoning, excessive agency, 법무 hallucination, procurement data quality, package hallucination, 보안 검증 부채, 개인정보/규제 리스크다.

| Researcher | Negative Search 수행 여부 | 주요 반례 축 | 결론에 준 영향 |
| --- | --- | --- | --- |
| R1 | 수행 | METR 19% slowdown, RPA 실패율, 자동화 유지보수 실패, Power Automate 한계 | 평균 ROI 단정 금지, task selection과 ownership 강조. |
| R2 | 수행 | 제품별 한계, 직접 비교 부재, APEX 낮은 완료율, prompt injection, auto mode permission gap | full automation 대신 감독형 운영 모델 권고. |
| R3 | 수행 | MCP 보안, GitHub Actions 권한, n8n/Zapier/Claude Action friction, 감사 로그 부족 | event-agent-verify-approve-audit 구조 강화. |
| R4 | 수행 | legal hallucination, procurement failure, RPA governance, AI code security, enterprise AI adoption barrier | Top 10을 검토 가능한 산출물과 승인 패킷 중심으로 제한. |
| R5 | 수행 | Codex/Claude/GitHub 위험 문서, prompt injection, MCP exploit, package hallucination, METR, RAND/BCG/McKinsey | 권한 tier, ROI dashboard, 30/60/90일 제한 파일럿 제안. |

### Critic focus 제안

1. 벤더 고객사례 수치를 최종 리포트에서 어느 강도로 표현할지 검토해야 한다. `효과 패턴 근거`와 `정량 ROI 근거`를 분리하는 것이 중요하다.
2. GitHub-Accenture와 METR의 생산성 상충을 조건 차이로 해석해도 되는지 확인해야 한다.
3. R2의 최신 제품 방향 중 2026년 날짜와 기능 표현이 내부 산출물 기준으로 충분히 일관적인지 확인해야 한다.
4. R3의 표준 아키텍처가 모든 직무에 과도하게 일반화되지 않았는지 검토해야 한다.
5. R4 Top 10 우선순위가 근거 강도보다 기대 가치에 끌려 올라간 항목은 없는지 봐야 한다.
6. 법무, 구매, 재무, 산업운영 후보는 `자동 실행`이 아니라 `승인 패킷 생성`으로 충분히 낮춰 표현됐는지 확인해야 한다.
7. R5의 T0-T4 권한 tier와 30/60/90일 파일럿이 실무적으로 실행 가능한지, 또는 과도한 통제 비용을 만들 수 있는지 검토해야 한다.
8. 외부 심층리서치가 필요하다면 우선순위는 `장기 운영 데이터`, `독립 ROI`, `동일 조건 제품 비교`, `guardrail 비용`이다.

## 9. Synthesis 참고사항

최종 종합 리포트는 모델이나 제품 비교보다 운영 모델을 중심에 두는 편이 안전하다. 다섯 산출물의 공통 결론은 다음 문장으로 압축된다. “AI 자동화와 코딩 에이전트의 실전 가치는 사람이 검토할 수 있는 산출물, 자동 검증, 승인 게이트, 감사 로그가 있는 반복 업무에서 먼저 나온다.”

최종 리포트에서 강하게 말해도 되는 내용은 기능 방향, 안전 설계 원칙, 권한 tier, 검토 가능한 산출물 중심의 use case 선정이다. 약하게 말해야 하는 내용은 벤더별 ROI 크기, 제품별 우열, 전사 평균 생산성 향상, 고위험 업무의 자동 의사결정 가능성이다.

Synthesis 초안 구조 후보:

1. 왜 지금 AI 자동화와 코딩 에이전트를 함께 봐야 하는가.
2. 성공 패턴: 반복 업무를 산출물, 검증, 승인, 로그로 바꾸는 방식.
3. 우선 도입 후보: 개발/IT, SecOps, supplier onboarding, contract redline, finance close 등.
4. 표준 아키텍처: workflow platform, context/MCP, coding agent, CI/validation, human approval, deterministic action, audit ledger.
5. 운영 통제: T0-T4 권한 tier, 데이터/네트워크/도구/MCP governance, legal/privacy gate.
6. ROI 측정: baseline, throughput, review time, rework, defect/security, cost, incident/near miss.
7. 90일 실행안: T0-T2 제한 파일럿에서 시작하고 T3/T4 직접 실행은 보류.

## 10. Pass 2 업데이트

Critic은 Synthesis를 `조건부 가능`으로 판정했다. 조건은 세 가지였다. 첫째, 벤더 고객사례의 절감 수치를 평균 ROI처럼 쓰지 않는다. 둘째, Top 10/18개 유즈케이스에 직접 근거, 인접 근거, 합성 추론 라벨을 붙인다. 셋째, 법무/구매/재무/산업운영은 자동 실행이 아니라 승인 패킷, redline, memo, work order 초안 중심으로 표현한다.

Repair Queue는 별도 Verifier가 필요한 원문 오류가 아니라 Synthesis 문장 강도 보정 문제로 처리했다. `00-final-synthesis.md`는 Critic 권고에 따라 15개 유즈케이스 표에 근거 등급을 붙였고, 제품 우열 결론을 내리지 않았으며, vendor-only 수치는 사례 가능성으로만 사용했다.

External Deep Research Gate는 열지 않았다. 남은 gap은 결합 워크플로우의 6-12개월 장기 운영 사례, 독립 ROI 검증, 제품별 동일 조건 비교인데, 현재 사용자 요구는 "검증된 ROI 순위"가 아니라 "혁신적 유즈케이스와 실행안"이므로 blocking gap이 아니다.

| 항목 | 최종 상태 | 메모 |
| --- | --- | --- |
| Critic findings | 완료 | `99-critic-review.md` 작성. 조건부 진행 가능. |
| Repair Queue | Synthesis 반영 완료 | 근거 등급, vendor-only 제한, 자동 실행 경계 반영. |
| Expansion Queue | deferred | 장기 운영 ROI와 제품 비교는 후속 리서치 과제. |
| Verifier corrections | 미수행 | 원문 수치 오류 대조가 아니라 문장 강도 보정 사안이었다. |
| Final synthesis | 완료 | `00-final-synthesis.md` 작성. |
