# R5 발전 방향과 임팩트 모델 - 코딩 에이전트/업무 에이전트의 업무 개선과 자동화

**Researcher**: R5  
**Mode**: mixed  
**Date**: 2026-04-22  
**Scope**: 2026년 기준 향후 1-3년 코딩 에이전트와 업무 에이전트의 발전 방향, 기업 생산성/조직 구조/역량 모델 영향. 포함 범위는 모델 성능, 멀티에이전트, 장기 실행, tool use, sandbox, enterprise governance, human-in-the-loop, AI-native 운영체계, ROI 프레임이다. 최종 synthesis가 아니라 R5 관점의 bounded Researcher 산출물이다.

## 핵심 요약

- 더 나은 문제 정의: "코딩 에이전트가 개발자를 대체하는가?"보다 "어떤 업무 단위가 에이전트에게 위임 가능한 work package가 되며, 어떤 거버넌스와 측정 체계가 있어야 손익 영향으로 전환되는가?"가 더 의사결정에 유용하다.
- 2026년 제품 방향은 단순 코드 자동완성에서 벗어나, 장기 실행/기억/컴퓨터 사용/멀티툴/Slack·GitHub·Notion·Gmail 같은 업무 표면 연결로 이동하고 있다. OpenAI Codex의 2026년 업데이트는 컴퓨터 사용, 미래 작업 예약, 기억, PR 리뷰, SSH devbox, 문서·스프레드시트·슬라이드 미리보기까지 포함한다. Anthropic은 Claude Code의 subagent, tool permission, hooks, Agent SDK를 공개했고, Microsoft는 Copilot Studio의 multi-agent orchestration과 Entra Agent ID/Purview governance를 공식화했다.
- 생산성 임팩트는 "개인 속도 향상"만으로 설명하기 어렵다. Accenture/GitHub, allpay, Dow, Reddit/OpenTable 같은 사례는 만족도, 반복업무 절감, 백오피스/지원 자동화의 비용 효과를 보여준다. 반면 METR RCT는 2025년 초 도구가 숙련 오픈소스 개발자에게 19% 지연을 만들었다고 보고했고, Gartner/MIT NANDA는 agent washing, ROI 부재, workflow integration gap을 강하게 경고한다.
- 향후 1-3년의 핵심 변화는 조직도가 "사람 역할" 중심에서 "사람+에이전트가 맡는 작업 큐, 승인권한, 관측가능성, 비용 한도" 중심으로 재설계되는 것이다. Microsoft Work Trend Index는 31개국 31,000명 조사에서 리더 81%가 12-18개월 내 에이전트를 AI 전략에 중등도 이상 통합할 것으로 본다고 보고했다. 단, 이는 벤더 후원 조사이며 실제 손익 효과는 업무별로 검증해야 한다.

## 주요 발견

### 1. 제품 로드맵은 "코드 작성 도구"에서 "업무 운영 인터페이스"로 이동한다

- **Fact**: OpenAI Codex는 2025년 GA에서 Slack delegation, Codex SDK, environment controls, monitoring, analytics dashboards를 발표했고, 2026년에는 컴퓨터 사용, 기억, 자동화 재개, 여러 터미널/파일/브라우저/remote devbox 지원을 공개했다. 이는 coding agent가 소스 편집기 안에 머무르지 않고 업무 도구와 의사결정 흐름으로 들어가는 방향이다.
- **Fact**: GPT-5.2-Codex와 GPT-5.3-Codex 발표는 long-horizon work, context compaction, tool calling, terminal use, cybersecurity capabilities를 전면에 둔다. OpenAI는 GPT-5.3-Codex가 "코드를 쓰는 것"을 넘어 컴퓨터를 조작해 end-to-end 업무를 완료하는 쪽으로 이동한다고 설명했다.
- **Fact**: Claude Sonnet 4.5/Claude Code는 30시간 이상 장기 작업, subagent, permission, hooks, Agent SDK를 강조한다. Claude Code 문서는 subagent가 별도 context에서 독립 작업하고, tool allowlist/denylist와 fine-grained permissions로 제약될 수 있음을 명시한다.
- **Fact**: Microsoft Copilot Studio는 multi-agent orchestration, Entra Agent ID, Purview Information Protection을 공개했다. 이 조합은 에이전트를 "사용자 없는 자동화"가 아니라 신원, 권한, 데이터 보호, 감사 대상인 first-class business entity로 취급하는 방향을 보여준다.

### 2. 임팩트 모델은 4단계로 보는 것이 적합하다

1. **개인 증강**: 코드 작성, 테스트, 문서화, 분석, 리서치 등 개인 업무의 보조. ROI는 시간 절감과 만족도 중심이며 측정이 쉽지만 과대평가가 잦다.
2. **작업 패키지 위임**: 이슈 수정, PR 리뷰 대응, CI 실패 요약, 릴리스 브리프, 고객문의 초안 등 명확한 완료조건이 있는 작업을 에이전트에게 맡긴다. human-in-the-loop 검토와 sandbox가 필수다.
3. **워크플로 자동화**: 채널, 티켓, 저장소, 문서, ERP/CRM 사이를 에이전트가 오가며 업무 상태를 갱신한다. Codex automations, Copilot Studio autonomous agents, Agentforce 2dx가 이 방향이다.
4. **AI-native 운영체계**: 조직이 업무 큐, 권한, 로그, 비용, 품질 기준, 승인을 사람+에이전트 혼합 팀 기준으로 재설계한다. 이 단계에서는 생산성보다 cycle time, 품질, risk-adjusted throughput, external spend 절감이 핵심 KPI가 된다.

### 3. 기업 생산성 영향은 "많이 만든다"보다 "검토·운영 병목을 어디로 이동시키는가"가 중요하다

- 코딩 에이전트는 산출물 생성을 늘리지만, 병목이 설계 검토, 보안 검토, 테스트, 제품 판단, 코드 소유권으로 이동할 수 있다. GitHub Well-Architected는 에이전트가 이미 많은 조직에서 PR volume 기준 주요 contributor가 되고 있으며, audit log, SIEM, foundational code security practice 위에 agent governance를 추가해야 한다고 권고한다.
- GitHub Copilot/Accenture 연구는 90%가 직무 만족 증가, 95%가 coding enjoyment 증가, 67%가 주 5일 이상 사용을 보고했다. 그러나 이는 경험·채택 지표가 강하고 순수 생산성 효과는 해석상 주의가 필요하다.
- METR의 RCT는 숙련 개발자가 자기 저장소의 실제 이슈를 처리할 때 AI 허용 조건이 19% 느렸다고 보고했다. 이는 "도구가 나쁨"의 일반 결론이 아니라, 고숙련/고맥락/대형 mature repo에서는 verification tax와 맥락 부족이 속도 이익을 상쇄할 수 있다는 반례다.

### 4. 조직 구조와 역량 모델은 "에이전트 관리자"가 아니라 "work system designer" 쪽으로 변한다

- 향후 필요한 역량은 프롬프트 작성보다 업무 분해, acceptance criteria 작성, tool permission 설계, eval/rollback, observability, 데이터 접근권 관리, 비용-품질 trade-off 조정이다.
- Stanford WORKBank는 1,500명 근로자, 104개 직업, 844개 작업과 52명 AI 전문가 주석을 바탕으로 AI agent capabilities와 worker preferences를 비교하며, 핵심 인간 역량이 정보처리에서 대인·조직 역량으로 이동할 수 있다고 본다.
- Microsoft Work Trend Index의 "Frontier Firm" 개념은 2-5년 내 조직이 사람+AI agent 팀으로 전환된다는 강한 가설을 제시한다. 다만 이는 Microsoft 생태계 관점의 vendor report이므로, 실제 조직 구조 변화의 강도는 산업별 규제, 데이터 성숙도, 노무·보상 체계에 따라 달라진다.

### 5. ROI 프레임은 업무별 "Agentic ROI"로 분해해야 한다

- arXiv position paper "The Real Barrier to LLM Agent Usability is Agentic ROI"는 핵심 질문이 "자동화 가능한가"가 아니라 "가치가 비용과 위험을 초과하는가"라고 주장한다.
- 권장 프레임: `Agentic ROI = (시간 절감 + cycle time 단축 + 품질/리스크 개선 + 외부비용 절감 + 매출/전환 개선 - 검토/운영/토큰/라이선스/오류비용) / 총도입비용`.
- 선행 적용 후보는 반복적이고 완료조건이 명확하며, 실패 시 rollback 가능하고, 데이터 접근권을 제한할 수 있는 업무다. 예: PR 리뷰 코멘트 처리, 테스트 생성, CI 실패 triage, 송장 검증, 고객지원 deflection, 내부 지식 질의, 문서·스프레드시트 초안.
- 후순위 또는 신중 적용 후보는 ambiguous ownership, 고위험 의사결정, 법적 책임, 대규모 side effect가 있는 업무다. 이 경우 에이전트는 autonomous actor보다 recommendation engine 또는 supervised operator로 둔다.

## 근거 표

| 주장 | 근거 | 출처 유형 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| 코딩 에이전트는 IDE 보조에서 Slack/GitHub/문서/컴퓨터 조작을 포함하는 업무 운영 인터페이스로 확장 중 | Codex GA: Slack integration, SDK, admin tools. 2026 Codex: computer use, memory, scheduled automations, PR review, remote devboxes | official / release note | 높음 | https://openai.com/index/codex-now-generally-available/ ; https://openai.com/index/codex-for-almost-everything/ |
| 모델 성능 발전의 초점은 long-horizon, context compaction, tool calling, terminal use, cyber capability | GPT-5.2-Codex/5.3-Codex 발표에서 장기 작업, compaction, tool calling, cybersecurity 강조 | official / release note | 높음 | https://openai.com/index/introducing-gpt-5-2-codex/ ; https://openai.com/index/introducing-gpt-5-3-codex/ |
| Claude Code 계열은 장기 실행, subagent, permission, hooks, Agent SDK로 agent infrastructure화 | Sonnet 4.5 발표 및 Claude Code 문서: 30시간 이상 작업, subagent, tool restriction, fine-grained permission | official / docs | 높음 | https://www.anthropic.com/news/claude-sonnet-4-5 ; https://docs.anthropic.com/en/docs/claude-code/sub-agents ; https://docs.anthropic.com/en/docs/claude-code/team |
| 엔터프라이즈 에이전트는 신원·권한·감사·정보보호 레이어를 필요로 한다 | Microsoft Build 2025: multi-agent orchestration, Entra Agent ID, Purview Information Protection. GitHub governance: audit log/SIEM/security practice 위 agent governance | official / governance | 높음 | https://www.microsoft.com/en-us/microsoft-365/blog/2025/05/19/introducing-microsoft-365-copilot-tuning-multi-agent-orchestration-and-more-from-microsoft-build-2025/ ; https://wellarchitected.github.com/library/governance/recommendations/governing-agents/ |
| 업무 임팩트는 직무별로 이질적이며 초보/저숙련자에게 더 큰 생산성 효과가 나타날 수 있다 | NBER customer support field study: 평균 14% 생산성 증가, novice/low-skilled 34%, skilled worker 효과 미미 | academic / field study | 중상 | https://www.nber.org/papers/w31161 |
| 숙련 개발자/대형 mature repo에서는 AI가 속도를 늦출 수 있다 | METR RCT: 16명, 246개 실제 작업, 평균 5년 repo 경험, AI 허용 시 19% 느림 | academic / RCT | 중상 | https://arxiv.org/abs/2507.09089 |
| 2026년 이후 측정은 어려워진다. AI 미사용 조건을 거부하거나 AI가 유리한 task를 표본에서 제외하는 선택효과가 커짐 | METR 2026 update: 2025년 하반기 연구에서 selection effects와 multi-agent 병행 사용 때문에 task-level productivity 측정이 불안정 | research org / methodology update | 중 | https://metr.org/blog/2026-02-24-uplift-update/ |
| 에이전트 도입은 정보처리 역량보다 대인·조직 역량의 중요성을 높일 수 있다 | Stanford WORKBank: 104개 직업, 844개 작업, 1,500명 근로자, 52명 AI 전문가 | academic / workforce study | 중 | https://futureofwork.saltlab.stanford.edu/ |
| 직접 사례에서 효과는 반복 업무·백오피스·지원 자동화에 강하게 나타난다 | allpay: GitHub Copilot으로 전체 개발 생산성 10%, 일부 use case 80% time saving. Dow: 100,000개 이상 송장 분석 agent로 몇 주/몇 달 작업을 minutes 단위로 단축, 첫해 수백만 달러 절감 기대. Salesforce Agentforce: Reddit 46% deflection, 84% resolution time reduction | direct case / stakeholder | 중 | https://www.allpay.net/news/allpay-boosts-productivity-by-10-with-github-copilot-a-case-study-with-microsoft/ ; https://blogs.microsoft.com/blog/2025/04/28/how-agentic-ai-is-driving-ai-first-business-transformation-for-customers-to-achieve-more/ ; https://investor.salesforce.com/news/news-details/2025/Welcome-to-the-Agentic-Enterprise-With-Agentforce-360-Salesforce-Elevates-Human-Potential-in-the-Age-of-AI/ |
| 과장 위험은 크며 agent washing과 ROI 부재가 실제 실패 원인으로 보고됨 | Gartner: 2027년 말까지 agentic AI project 40% 이상 취소 예측, agent washing 지적. MIT NANDA: $30-40B 투자에도 95% zero return/5% production 수준 주장 | analyst/report | 중 | https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027 ; https://www.artificialintelligence-news.com/wp-content/uploads/2025/08/ai_report_2025.pdf |

## 출처 품질 매트릭스

| 출처 유형 | 개수 | 핵심 기여 | 약점 |
| --- | ---: | --- | --- |
| official / primary | 10 | OpenAI, Anthropic, Microsoft, GitHub, Google, Salesforce의 제품 방향·릴리스·거버넌스 확인 | 벤더의 미래상과 성과 수치는 제품 채택을 유도하는 framing이 강함 |
| academic / standard / patent | 7 | METR RCT, NBER field study, Stanford WORKBank, arXiv Agentic ROI/AIDev/Fingerprinting/업무자동화 사례로 실증·방법론 제공 | 빠르게 변하는 2026년 제품 성능을 즉시 반영하지 못하거나 peer review 전 논문 포함 |
| direct case / experiment | 6 | allpay, Dow, Reddit, OpenTable, Accenture/GitHub, Company S expense processing 등 업무별 성과 | 대체로 vendor customer story이거나 self-reported이며 통제군 부족 |
| vendor / stakeholder | 8 | 실제 제품 로드맵, 가격/가용성, governance feature, 사용 사례를 가장 직접적으로 제공 | ROI와 성능 과장 가능성, 실패 사례 비공개 |
| community | 3 | Claude/GitHub/Salesforce 사용자의 permission, latency, forced AI, support bot 실패 경험 확인 | 익명·표본 편향, 검증 어려움. 차단 도메인은 사용하지 않음 |
| weak / unverified | 2 | MIT NANDA PDF mirror, 일부 언론 재인용으로 원문 접근 보완 | 원 배포 경로·방법론 세부 검증 필요. 결론에는 중간 확신도로만 반영 |

## 반례/실패 사례 검색 로그

| 쿼리 | 목적 | 결과 | 결론 영향 |
| --- | --- | --- | --- |
| `AI agents hype cycle failure Gartner 2025 agent washing ROI` | agent hype와 취소 전망 확인 | Gartner가 2027년 말까지 40% 이상 agentic AI project 취소, agent washing, ROI 부족을 발표 | ROI 모델에 "agent가 필요한 업무인지" 판별 게이트 추가 |
| `AI agent ROI failure MIT NANDA 2025 report 95% enterprise genAI pilots` | 기업 AI pilot 실패율·원인 확인 | MIT NANDA PDF/언론 재인용에서 95% zero return, 5% integrated pilots extracting value, workflow learning gap 주장 | 대규모 확장 전 workflow integration, memory, feedback learning 검증 필요 |
| `coding agents not autonomous METR experienced developers slower 2025` | 코딩 에이전트 생산성 반례 확인 | METR RCT: 숙련 OSS 개발자 실제 작업에서 19% 느림 | "개발 생산성 자동 증가" 주장을 기각하고 task/context별 평가로 전환 |
| `enterprise AI adoption barriers governance data privacy risk management Deloitte 2025` | 엔터프라이즈 도입 장벽 확인 | Deloitte/Forrester/Microsoft 자료에서 governance, trust, data, training, security가 반복 등장 | enterprise governance와 human-in-the-loop를 필수 전제에 포함 |
| `generative AI pilot failure workflow integration memory learning gap` | pilot-to-production 실패 원인 확인 | MIT NANDA: brittle workflow, lack of contextual learning, misalignment with day-to-day operations | "챗봇 데모"와 "운영 시스템" 사이의 격차를 핵심 불확실성으로 기록 |
| `Claude Code permission sandbox failure subagent permission chaos` | sandbox/permission 실패 가능성 탐색 | Reddit 등에서 subagent permission, sandbox, hook 관련 불만이 발견되나 공식 incident로 확정하기 어려움 | 커뮤니티 증거로만 반영. 권한 자동화는 fail-closed 설계 필요 |
| `GitHub Copilot agent production code context limit enterprise codebase` | 대형 codebase 한계 확인 | Reddit/언론에서 context limit, output quality, forced Copilot UI 불만 확인 | governance와 adoption consent, code owner review를 의사결정 영향에 포함 |
| `Agentforce ROI hype support case failure slow latency` | 업무 에이전트 실패·과장 가능성 확인 | Salesforce 커뮤니티에서 느린 응답, demo 중심, 데이터/flow 미성숙 비판 확인 | 고객지원 agent는 knowledge/data hygiene 없으면 역효과 가능 |

## 상충점과 불확실성

- **성능 시간차**: METR의 2025년 초 RCT는 Cursor Pro와 Claude 3.5/3.7 Sonnet 중심이고, 2026년 Codex/Claude/Gemini 계열 장기 실행 모델과 agent scaffolding을 완전히 반영하지 않는다. METR 스스로도 2026년 업데이트에서 최신 도구가 더 빠를 가능성은 있으나 selection effect 때문에 추정이 어렵다고 밝혔다.
- **벤더 성과 vs 독립 검증**: allpay, Dow, Reddit, OpenTable, Salesforce, OpenAI internal Codex 사례는 직접 사례지만 이해관계자 자료다. 숫자는 유용하나 통제군·품질보정·장기 유지비가 부족하다.
- **생산성 측정 단위**: 코드 라인, PR 수, task completion time, cycle time, incidents, customer resolution, external spend reduction은 서로 다른 지표다. agent 도입은 output volume을 늘리면서 review load와 technical debt를 늘릴 수 있다.
- **조직 영향의 방향**: 고객지원/백오피스는 headcount와 outsourcing 비용 절감으로 이어질 가능성이 크지만, 소프트웨어 조직은 즉시 감원보다 "더 많은 실험/테스트/마이그레이션/보안수정"으로 demand expansion이 생길 수 있다.
- **governance 미성숙**: agent identity, MCP/tool allowlist, sandbox, audit log, rollback, data classification이 없으면 ROI보다 보안·컴플라이언스 비용이 커질 수 있다.
- **AI-native 운영체계의 실증 부족**: "Frontier Firm"과 "agentic enterprise"는 방향성은 강하지만 아직 2026년 기준 장기 패널 데이터가 부족하다.

## 의사결정 영향

- 2026-2027년 투자는 전사 "AI agent" 플랫폼보다, 완료조건·데이터 접근권·rollback이 명확한 5-10개 workflow를 골라 측정하는 방식이 적합하다.
- 코딩 조직의 우선 적용 영역은 PR 리뷰 코멘트 처리, 테스트 보강, 문서/릴리스 브리프, dependency update, CI failure triage, migration scaffold다. architecture decision, production incident response, security-sensitive infra 변경은 승인권자를 명확히 둬야 한다.
- 거버넌스 기본선은 agent identity, least-privilege tool permission, sandboxed execution, audit log/SIEM, MCP allowlist, budget cap, eval suite, code owner review, emergency disable switch다.
- ROI는 개인 설문보다 업무 큐 단위로 측정해야 한다. 권장 KPI: lead time, rework rate, escaped defects, review hours, incident count, cycle time, support deflection, cost per resolved item, external agency/BPO spend, employee satisfaction.
- 역량 개발은 prompt 교육만으로 부족하다. 업무 분해, acceptance test 작성, 에이전트 로그 읽기, 실패 복구, 데이터 거버넌스, human review rubric이 핵심이다.
- 구매/구축 판단은 MIT NANDA가 지적한 learning gap을 기준으로 한다. 내부 구축은 workflow learning과 tool integration 역량이 없으면 pilot에 갇힐 위험이 높고, vertical SaaS/기성 플랫폼은 빠른 time-to-value가 가능하지만 lock-in과 데이터 경계 문제가 생긴다.

## 인접 질문

1. 같은 개발 조직에서 "에이전트가 생성한 PR 수"가 늘어날 때 code review, QA, 보안검토, product discovery 병목은 어디로 이동하는가?
2. agent identity와 non-human workforce governance를 HR/IT/security가 공동 소유할 때, 권한·성과·책임·감사 체계를 어떤 조직 단위가 관리해야 하는가?

## 출처 목록

| # | 출처 | 날짜/버전 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| 1 | OpenAI, Codex is now generally available | 2025-10-06 | 높음 | https://openai.com/index/codex-now-generally-available/ |
| 2 | OpenAI, Codex for (almost) everything | 2026-04-16 | 높음 | https://openai.com/index/codex-for-almost-everything/ |
| 3 | OpenAI, Introducing GPT-5.2-Codex | 2025-12 | 높음 | https://openai.com/index/introducing-gpt-5-2-codex/ |
| 4 | OpenAI, Introducing GPT-5.3-Codex | 2026-02 | 높음 | https://openai.com/index/introducing-gpt-5-3-codex/ |
| 5 | OpenAI, New tools for building agents | 2025-03-11 | 높음 | https://openai.com/index/new-tools-for-building-agents/ |
| 6 | Anthropic, Introducing Claude Sonnet 4.5 | 2025-09-29 | 높음 | https://www.anthropic.com/news/claude-sonnet-4-5 |
| 7 | Anthropic Docs, Claude Code subagents | accessed 2026-04-22 | 높음 | https://docs.anthropic.com/en/docs/claude-code/sub-agents |
| 8 | Anthropic Docs, Claude Code team/IAM permissions | accessed 2026-04-22 | 높음 | https://docs.anthropic.com/en/docs/claude-code/team |
| 9 | Microsoft 365 Blog, Copilot Tuning and multi-agent orchestration | 2025-05-19 | 높음 | https://www.microsoft.com/en-us/microsoft-365/blog/2025/05/19/introducing-microsoft-365-copilot-tuning-multi-agent-orchestration-and-more-from-microsoft-build-2025/ |
| 10 | GitHub Well-Architected, Governing agents in GitHub Enterprise | 2026-04-13 | 높음 | https://wellarchitected.github.com/library/governance/recommendations/governing-agents/ |
| 11 | Google, Jules is now available | 2025-08 | 중상 | https://blog.google/innovation-and-ai/models-and-research/google-labs/jules-now-available/ |
| 12 | Microsoft Work Trend Index 2025 | 2025 | 중 | https://www.microsoft.com/en-us/worklab/work-trend-index/2025-the-year-the-frontier-firm-is-born |
| 13 | Gartner, 40%+ agentic AI projects canceled by end 2027 | 2025-06-25 | 중상 | https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027 |
| 14 | MIT NANDA, The GenAI Divide: State of AI in Business 2025 | 2025-07 | 중 | https://www.artificialintelligence-news.com/wp-content/uploads/2025/08/ai_report_2025.pdf |
| 15 | METR/arXiv, Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity | 2025-07 | 중상 | https://arxiv.org/abs/2507.09089 |
| 16 | METR, Changing developer productivity experiment design | 2026-02-24 | 중상 | https://metr.org/blog/2026-02-24-uplift-update/ |
| 17 | NBER, Generative AI at Work | 2023, revised | 높음 | https://www.nber.org/papers/w31161 |
| 18 | OECD AI Papers, The effects of generative AI on productivity, innovation and entrepreneurship | 2025 | 중상 | https://www.oecd.org/content/dam/oecd/en/publications/reports/2025/06/the-effects-of-generative-ai-on-productivity-innovation-and-entrepreneurship_da1d085d/b21df222-en.pdf |
| 19 | Stanford SALT Lab, Future of Work with AI Agents / WORKBank | 2025 | 중 | https://futureofwork.saltlab.stanford.edu/ |
| 20 | arXiv, The Real Barrier to LLM Agent Usability is Agentic ROI | 2025-05 | 중 | https://arxiv.org/abs/2505.17767 |
| 21 | arXiv, AIDev: Studying AI Coding Agents on GitHub | 2026-02 | 중 | https://arxiv.org/abs/2602.09185 |
| 22 | arXiv, Fingerprinting AI Coding Agents on GitHub | 2026-01 | 중 | https://arxiv.org/abs/2601.17406 |
| 23 | arXiv, E2E Process Automation Leveraging Generative AI and IDP-Based Automation Agent | 2025-05 | 중 | https://arxiv.org/abs/2505.20733 |
| 24 | allpay, GitHub Copilot case study with Microsoft | 2025-03-13 | 중 | https://www.allpay.net/news/allpay-boosts-productivity-by-10-with-github-copilot-a-case-study-with-microsoft/ |
| 25 | Microsoft Official Blog, agentic AI customer transformation | 2025-04-28 | 중 | https://blogs.microsoft.com/blog/2025/04/28/how-agentic-ai-is-driving-ai-first-business-transformation-for-customers-to-achieve-more/ |
| 26 | Salesforce investor release, Agentforce 360 customer results | 2025 | 중 | https://investor.salesforce.com/news/news-details/2025/Welcome-to-the-Agentic-Enterprise-With-Agentforce-360-Salesforce-Elevates-Human-Potential-in-the-Age-of-AI/ |
| 27 | GitHub Blog, Quantifying Copilot impact with Accenture | 2024-05-13 | 중 | https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-in-the-enterprise-with-accenture/ |
| 28 | GitHub/Forrester TEI, GitHub Enterprise Cloud ROI | 2025-08-21 | 중 | https://github.com/resources/whitepapers/forrester |
| 29 | Forrester Consulting commissioned by Microsoft, Projected TEI of Copilot Studio | 2025-06 | 중 | https://tei.forrester.com/go/Microsoft/CopilotStudio/docs/Forrester_TEI_New_Technology__The_Projected_Total_Economic_Impact%E2%84%A2_Of_Microsoft_Copilot_Studio_vA.pdf |

## 검색 포화 판단

- 검색 깊이 게이트 충족: official/product roadmap 또는 release note 3개 이상, analyst/report/academic 3개 이상, 직접 adoption/ROI 사례 2개 이상, 실패/과장 가능성 검색 2개 이상을 충족했다.
- 포화 근거: OpenAI/Anthropic/Microsoft/GitHub/Google/Salesforce의 공식 자료가 반복적으로 같은 방향(장기 실행, tool use, 멀티에이전트, governance)을 제시했고, 독립 연구/보고서도 같은 긴장점(ROI, workflow integration, governance, human-in-the-loop)을 반복했다. 추가 검색은 새로운 증거 유형보다 vendor/customer story의 중복을 늘릴 가능성이 높다.
- 아직 직접 증거가 부족한 항목: 2026년형 Codex/Claude Code/GitHub Copilot coding agent를 동일 조직·동일 업무에서 비교한 head-to-head field experiment, multi-agent orchestration이 조직 구조를 바꾼 장기 패널 데이터, agent-caused incident의 공개 통계.
- 다음 라운드 질문: "agent-generated PR 비중이 20% 이상인 조직에서 defect/rework/security finding은 어떻게 변하는가?", "agent identity와 human accountability를 감사 가능한 방식으로 연결하는 enterprise reference architecture는 무엇인가?"
