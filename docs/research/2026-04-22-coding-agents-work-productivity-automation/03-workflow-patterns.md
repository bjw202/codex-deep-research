# 업무 플로우/자동화 패턴 - 코딩 에이전트 기반 업무 생산성 자동화

**Researcher**: R3  
**Mode**: mixed  
**Date**: 2026-04-22  
**Scope**: Codex, Claude Code, GitHub Copilot 같은 코딩 에이전트가 소프트웨어 개발을 넘어 문서, 스프레드시트, 슬라이드, 대시보드, ETL, 내부도구, 테스트, 모니터링, 데이터 검증, PR/이슈 자동화, 브라우저/데스크톱 업무 자동화로 확장되는 패턴을 조사한다. 최종 synthesis가 아니라 R3 관점의 bounded Researcher 산출물이다.

## 핵심 요약

코딩 에이전트가 일반 업무 혁신에 강한 이유는 “텍스트 생성기”라서가 아니라, 업무 산출물을 파일/코드/데이터/브라우저 동작으로 다루고 검증 루프를 붙일 수 있기 때문이다. OpenAI Codex 문서는 Codex가 코드 읽기/수정/실행뿐 아니라 슬라이드, Gmail 초안, QA 리포트, 탭ular 데이터 질의, 피드백 정리 같은 업무 산출물을 다루는 use case를 공식화한다. Claude Code와 GitHub Copilot도 PR, 문서, 테스트, GitHub Actions, 이슈-브랜치-PR 흐름을 제품 문서의 중심 워크플로우로 제시한다.

가장 재사용 가능한 패턴은 “의도 입력 → 컨텍스트 수집 → 산출물 생성 → 자동 검증 → 사람이 승인/수정 → 반복 업무는 스킬/워크플로우로 저장”이다. 이 패턴은 PR 자동화뿐 아니라 PPT 생성, 이메일 triage, QA, SQL/데이터 분석, 내부도구 조작, 알림/이슈 triage에도 적용된다. Zapier Agents, n8n AI Agent Tool, Microsoft Power Automate generative actions, GitHub Agentic Workflows는 같은 구조를 업무 자동화 플랫폼 쪽에서 구현한다.

다만 완전자율보다 bounded autonomy가 더 현실적이다. GitHub Copilot cloud agent는 단일 저장소/단일 브랜치/단일 PR 제약과 content exclusion 미반영 같은 한계를 명시한다. Microsoft Power Automate generative actions도 preview, 텍스트 입력, 제한된 connector, 별도 취소, DLP 한계를 밝힌다. NIST와 OWASP는 tool use, excessive agency, hallucination, 권한/정체성/감시 문제를 업무 자동화의 핵심 위험으로 본다.

## 주요 발견

1. **산출물 유형이 넓어질수록 코딩 에이전트의 장점은 “생성”보다 “구조화+검증”에서 나온다.**  
   Codex의 공식 use cases는 `.pptx` 편집, 이미지 생성, 슬라이드 렌더/오버플로우/폰트 검증, Gmail/Slack/Drive를 통한 이메일 초안, Computer Use 기반 QA 리포트, CSV/스프레드시트 질의, 피드백의 action item 변환을 포함한다. 이 범위는 업무 산출물을 코드처럼 읽고, 변환하고, 테스트하는 방식과 맞아떨어진다. 확신도: 높음.

2. **에이전트형 업무 자동화의 기본 단위는 “작업자”가 아니라 “리뷰 가능한 패치/초안/리포트”다.**  
   GitHub Copilot cloud agent와 Claude Code는 PR 생성, 테스트, 문서, 리뷰, GitHub Actions 실행을 공식 흐름으로 둔다. Codex도 cloud task, parallel background work, GitHub PR 생성, Slack/Linear/GitHub 연동, Skills를 반복 워크플로우의 authoring format으로 둔다. 일반 업무에 적용하면 이메일은 “보내기”보다 “초안 큐”, QA는 “자동 수정”보다 “재현 단계와 severity 리포트”, 데이터 분석은 “최종 의사결정”보다 “쿼리/노트북/검증 로그”가 안전한 산출물이다. 확신도: 높음.

3. **실제 사례는 자동화 가치가 ‘범용 자율성’보다 병목 제거에 있다는 점을 보여준다.**  
   Block의 goose는 Claude+Databricks+MCP를 통해 SQL, 데이터 접근, 내부 툴 연결, 운영 티켓 처리에 쓰였고 4,000명 수준의 내부 사용과 엔지니어 주당 8-10시간 절감 사례가 제시된다. Graphite와 CodeRabbit은 Claude 기반 코드 리뷰/수정 제안으로 PR 피드백 루프와 QA를 자동화했다. GitHub Copilot coding agent는 이슈를 체크리스트, 브랜치, PR, 테스트, 리뷰 사이클로 변환하는 운영 패턴을 제시한다. 확신도: 중상. 수치는 벤더/고객 사례라 독립 검증은 제한적이다.

4. **패턴 라이브러리는 “어떤 도구를 붙이느냐”보다 “검증 가능한 완료 조건을 어디에 두느냐”로 나뉜다.**

| 패턴 | 입력 | 에이전트가 만드는 산출물 | 검증/승인 게이트 | 적합한 업무 |
| --- | --- | --- | --- | --- |
| Issue-to-PR | 이슈, 요구사항, repo 규칙 | 브랜치, 커밋, PR, 체크리스트 | 테스트/린트, PR 리뷰, peer approval | 버그, 테스트, 문서, 단순 기능, 마이그레이션 |
| Docs-as-code | 코드/노트/마크다운 폴더 | README, API docs, changelog, JSDoc | 문서 표준 체크, 링크/예제 검토 | 온보딩, 릴리즈 노트, 운영 가이드 |
| Deck-as-code | 원본 PPT/PDF/메모/브랜드 가이드 | `.pptx`, 이미지, native charts | 렌더 PNG, overflow/font/layout 검사 | 주간/분기 보고, 영업 제안서, 교육자료 |
| Spreadsheet/data QA | CSV, Excel, DB export | 정제 스크립트, 요약표, 검증 로그 | schema/row count/reconciliation checks | 재무/운영 리포트, 데이터 검증, KPI 분석 |
| Browser/desktop QA | staging URL, 테스트 플랜 | 재현 단계, expected/actual, severity | 스크린샷/로그, 사람이 triage | 릴리즈 전 QA, UI 회귀, 설정 변경 |
| Inbox/message triage | Gmail/Slack/Drive | 응답 초안, 우선순위 큐, 맥락 링크 | “전송 금지” 기본값, 사용자 승인 | 이메일/문의 triage, 회의 follow-up |
| Alert/issue triage | CI, logs, Sentry, GitHub, Linear | 원인 가설, 이슈/PR draft, runbook update | read-only 우선, testable fix, escalation rule | 장애 대응, 보안/품질 부채 |
| Workflow-as-skill | 반복 프롬프트, 스크립트, 템플릿 | Skill/plugin, reusable workflow | 최소 예제, 실패 조건, 권한 범위 | 조직 표준 업무 자동화 |
| Multi-agent orchestration | 역할별 작업 큐 | specialist outputs, handoff logs | state trace, owner, retry/stop policy | 리서치, QA, 복잡한 백오피스 업무 |

5. **워크플로우 도구와 코딩 에이전트가 수렴하고 있다.**  
   Zapier Agents는 앱 연결, 지식 소스, actions, 버전 publish를 제공한다. n8n AI Agent Tool은 root agent가 다른 agent를 tool처럼 호출하는 multi-agent orchestration을 제공한다. Power Automate generative actions는 사용자가 intent만 정의하면 AI runtime이 action 순서를 선택하되 preview, run history, 제한 connector, DLP 한계를 둔다. GitHub Agentic Workflows는 `assign-to-agent`로 Copilot assignment를 workflow output으로 자동화한다. 코딩 에이전트는 여기에 파일 편집, 테스트 실행, PR, shell, structured validation을 더해 “업무 자동화의 구현/검증 계층”이 된다. 확신도: 높음.

6. **한계와 실패 모드는 권한, 상태, 컨텍스트, 검증의 문제로 수렴한다.**  
   OWASP는 LLM system이 tools/skills/plugins를 통해 외부 시스템과 상호작용할 때 excessive agency가 CIA 영향을 키운다고 본다. NIST GenAI Profile은 GenAI 리스크를 AI RMF로 관리해야 한다고 제시한다. GitHub 문서는 Copilot cloud agent가 단일 repo/branch/PR 단위로 제한되고 content exclusions를 반영하지 않는다고 명시한다. Power Automate는 generative actions가 preview이며 connector와 DLP 제약이 있음을 밝힌다. 학술 검색에서는 agentic PR의 실패 유형, CI/CD workflow reliability, agent autonomy risk가 별도 연구 주제로 등장했다.

## 근거 표

| 주장 | 근거 | 출처 유형 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| Codex는 background/parallel cloud task와 PR 생성에 적합하다 | Codex web 문서가 cloud environment, parallel background work, GitHub PR 생성을 설명 | official | 높음 | https://developers.openai.com/codex/cloud |
| Codex는 일반 업무 산출물까지 use case를 확장한다 | 공식 use case 목록에 slide decks, inbox, QA with Computer Use, tabular data, feedback actions, skills가 포함 | official | 높음 | https://developers.openai.com/codex/use-cases |
| 반복 업무는 skill/plugin으로 패키징 가능하다 | Codex Skills 문서가 instructions, resources, scripts, assets를 묶어 reusable workflow authoring format으로 설명 | official | 높음 | https://developers.openai.com/codex/skills |
| 슬라이드는 코드형 산출물로 자동화 가능하다 | Codex slide deck use case가 PptxGenJS, native charts, render, overflow/font checks를 권장 | official | 높음 | https://developers.openai.com/codex/use-cases/generate-slide-decks |
| 브라우저/데스크톱 업무는 Computer Use로 확장된다 | Codex Computer Use 문서가 GUI 조작, 브라우저, 설정 변경, 다중 앱 workflow, 권한 승인 필요성을 설명 | official | 높음 | https://developers.openai.com/codex/app/computer-use |
| QA 자동화는 structured bug report로 귀결되어야 한다 | Codex QA use case가 flow, repro steps, expected/actual, severity, triage summary를 명시 | official | 높음 | https://developers.openai.com/codex/use-cases/qa-your-app-with-computer-use |
| 이메일 triage는 보내기보다 초안/검토 큐가 안전하다 | Codex inbox use case가 Gmail/Slack/Drive context를 사용하되 drafts와 “Do not send anything” 패턴을 제시 | official | 높음 | https://developers.openai.com/codex/use-cases/manage-your-inbox |
| Agent Builder/Agents SDK는 workflow, tools, state, orchestration, guardrails를 제품 구조로 둔다 | OpenAI Agents SDK는 tool call, specialist handoff, state, trace를, Agent Builder는 visual workflow와 typed edges를 설명 | official | 높음 | https://developers.openai.com/api/docs/guides/agents / https://developers.openai.com/api/docs/guides/agent-builder |
| Claude Code는 문서/노트/이미지/PR/GitHub Actions에 걸친 workflow를 지원한다 | Claude Code common workflows는 documentation, non-code folders, image context, PR creation, MCP resources를 설명 | official | 높음 | https://code.claude.com/docs/en/tutorials |
| GitHub Copilot cloud agent는 repo 연구, 계획, branch change, PR, metrics, MCP/hooks/skills를 갖는다 | GitHub Docs가 cloud agent 기능, metrics, third-party integration, custom agents, hooks, limitations를 명시 | official | 높음 | https://docs.github.com/en/copilot/concepts/agents/cloud-agent/about-cloud-agent |
| GitHub issue-to-PR는 실무형 workflow 패턴이다 | GitHub Blog가 issue assignment → plan/checklist → branch/PR → tests/linters → review cycle을 설명 | official/stakeholder | 높음 | https://github.blog/ai-and-ml/github-copilot/assigning-and-completing-issues-with-coding-agent-in-github-copilot/ |
| 외부 workflow 플랫폼도 agent/tool/action 구조로 수렴한다 | Zapier Agents는 actions/knowledge sources/version publish, n8n은 multi-agent tool node, Power Automate는 generative action intent/action plan을 제공 | official | 높음 | https://help.zapier.com/hc/en-us/articles/24393442652557-Build-an-agent-in-Zapier-Agents / https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolaiagent/ / https://learn.microsoft.com/en-us/power-automate/generative-actions-overview |
| Block 사례는 코딩 에이전트가 데이터/내부 업무 자동화로 확장됨을 보여준다 | Claude+Databricks+goose가 SQL, data feature engineering, MCP internal tools, operations tickets에 쓰였고 4,000명 사용·엔지니어 절감 수치 제시 | direct case / vendor | 중상 | https://www.anthropic.com/customers/block |
| Graphite/CodeRabbit 사례는 code review를 workflow 병목으로 자동화한다 | Claude 기반 review가 PR feedback loop, bug/security detection, one-click fixes, Jira/Linear ticketing 연동으로 설명됨 | direct case / vendor | 중상 | https://www.anthropic.com/customers/graphite / https://www.anthropic.com/customers/coderabbit |
| agentic PR 연구는 높은 merge 가능성과 task별 차이를 동시에 보여준다 | AIDev 기반 연구들이 수천~수십만 agentic PR, task별 acceptance, failed PR categories, CI/CD workflow reliability를 분석 | academic | 중상 | https://arxiv.org/abs/2602.08915 / https://arxiv.org/abs/2601.15195 / https://arxiv.org/abs/2604.18334 |
| 자율 에이전트는 excessive agency와 autonomy risk가 핵심 위험이다 | NIST GenAI Profile, OWASP LLM Top 10 2025, OWASP Agentic App 자료, autonomy risk survey가 tool use/권한/감시 위험을 지적 | standard/academic | 높음 | https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence / https://owasp.org/www-project-top-10-for-large-language-model-applications/assets/PDF/OWASP-Top-10-for-LLMs-v2025.pdf / https://arxiv.org/abs/2506.23844 |

## 출처 품질 매트릭스

| 출처 유형 | 개수 | 핵심 기여 | 약점 |
| --- | ---: | --- | --- |
| official / primary | 17 | Codex, Claude Code, GitHub Copilot, Zapier, n8n, Power Automate, GitHub Agentic Workflows의 실제 기능·제약·workflow 구조 확인 | 벤더 문서는 제품 장점을 강조하며 실패율·운영비를 과소 설명할 수 있음 |
| academic / standard / patent | 8 | agentic PR, CI/CD reliability, autonomy risk, NIST/OWASP 보안·거버넌스 기준으로 한계 보정 | 일부 arXiv는 peer review 전이며 2026년 최신 연구는 아직 재현/반박 축적이 적음 |
| direct case / experiment | 5 | Block, Graphite, CodeRabbit, GitHub Copilot issue-to-PR, Codex workflow examples로 실제 병목과 산출물 패턴 연결 | 고객 사례의 수치는 vendor-reported이며 독립 감사 자료는 제한적 |
| vendor / stakeholder | 10 | 제품 구조, workflow recipe, 고객 quote, 운영 가이드 확보 | ROI와 성공 사례 편향 가능 |
| community | 4 | 자동화 실패, permission friction, 비용/요청량, n8n tool selection 문제 등 부정적 사용 경험 확인 | 익명/비대표 표본이며 환경 차이 큼 |
| weak / unverified | 2 | 최신 뉴스성 정황과 agentic hype/실패 담론 보조 | 핵심 주장에는 사용하지 않음 |

## 반례/실패 사례 검색 로그

| 쿼리 | 목적 | 결과 | 결론 영향 |
| --- | --- | --- | --- |
| `agentic workflow failure` | 자율 workflow 실패 유형 확인 | OWASP/NIST/CLTC 자료에서 tool misuse, excessive agency, cascading failure, oversight 부족이 반복적으로 등장 | “완전자율” 대신 권한 범위, action logging, approval gate 필요 |
| `RPA generative AI failure` | 전통 RPA+GenAI 실패 가능성 확인 | 커뮤니티/업계 자료에서 UI selector drift, silent failure, context drift, hallucinated action 우려 확인 | Computer Use/RPA형 자동화는 structured integration 우선, GUI는 마지막 수단 |
| `workflow automation hallucination` | hallucination이 업무 흐름으로 전파되는 위험 확인 | Trend Micro/OWASP/커뮤니티에서 자동화 간 연쇄 전파와 잘못된 정상 완료 문제가 제기됨 | 산출물 검증과 “모르면 멈춤/flag” 규칙이 필요 |
| `AI agent autonomy risk` | 자율성 자체의 위험 프레임 확인 | autonomy-induced security risk survey와 “fully autonomous agents should not be developed” 논문 확인 | bounded autonomy와 human responsibility가 핵심 설계 원칙 |
| `coding agent workflow limitation` | 코딩 에이전트 공식 한계 확인 | GitHub Docs가 단일 repo/branch/PR, content exclusion 미반영, GitHub-hosted repo 제약을 명시 | cross-repo/민감 파일/규정 기반 업무에는 별도 policy layer 필요 |
| `GitHub Copilot coding agent limitations content exclusions` | 제품별 반례 확인 | Copilot cloud agent limitations에서 content exclusions 미반영 확인 | 보안/컴플라이언스 도입 시 중요한 blocker |
| `Power Automate generative actions limitations` | enterprise workflow tool 한계 확인 | preview, text-only inputs, limited connectors, separate cancellation, DLP limitation 확인 | low-code AI automation도 생산 사용 전 제약 검토 필요 |
| `n8n AI Agent tool selection failure` | no-code/low-code agent 실패 확인 | 커뮤니티에서 tool selection, prompt following, token usage, parsing/schema drift 이슈 확인 | agent node만 믿지 말고 deterministic nodes와 schema validation 결합 필요 |
| `Claude Code automated workflow permission handling` | CLI automation friction 확인 | 커뮤니티에서 permission prompt 때문에 unattended workflow가 어렵다는 사례 확인 | headless/CI 자동화는 explicit permissions와 scoped tools 필요 |
| `AI coding agents failed pull requests GitHub` | 학술 반례 확인 | failed agentic PR 연구와 CI/CD reliability 연구 확인 | 문서/CI/build update는 강하고 bug/performance는 더 취약하다는 task stratification 반영 |

## 상충점과 불확실성

- **제품 문서는 자율성을 강조하지만, 운영 문서는 제한과 승인을 강조한다.** Codex/Copilot/Claude의 마케팅은 background teammate를 말하지만, 실제 문서의 안전한 완료 조건은 PR, draft, report, review, run history, permission prompt에 가깝다.
- **Block/Graphite/CodeRabbit의 수치는 강하지만 vendor-reported다.** 주당 절감 시간, 40x feedback loop, 86% faster delivery 같은 수치는 방향성 근거로 유용하나 독립 감사나 대조군은 제한적이다.
- **학술 근거는 소프트웨어 PR 중심이다.** 일반 업무 자동화(이메일, PPT, 내부도구, 브라우저 업무)의 대규모 공개 데이터셋은 아직 부족하다. 따라서 “코딩 에이전트가 일반 업무에서도 강하다”는 결론은 제품 기능과 사례의 구조적 유추가 섞여 있다.
- **workflow tool과 coding agent의 경계가 빠르게 바뀐다.** 2026년 4월 현재 Codex는 Computer Use, Skills, Automations, plugins를 넓히고 있고, GitHub는 Copilot 외 agent assignment도 넓히고 있다. 기능/가격/권한 정책은 단기간에 바뀔 수 있다.
- **반증 직접증거는 workflow 유형별로 불균형하다.** PR/CI 실패 연구는 강하지만, 슬라이드/이메일/스프레드시트 자동화의 공개 실패 데이터는 커뮤니티·일화성 자료 비중이 높다.

## 의사결정 영향

- 업무 자동화 후보는 “에이전트가 직접 완료해도 되는가”가 아니라 “리뷰 가능한 산출물과 검증 로그로 남길 수 있는가”로 선별해야 한다.
- 1차 도입 영역은 문서, 테스트, QA 리포트, PR/이슈 triage, 데이터 검증, 슬라이드 업데이트처럼 산출물이 명시적이고 되돌리기 쉬운 업무가 적합하다.
- 이메일 전송, 고객 데이터 수정, 회계/결제 변경, prod 설정 변경, 삭제/보안 액션은 기본적으로 draft/read-only/approval-first로 설계해야 한다.
- 반복 업무는 prompt만 저장하지 말고 skill 또는 workflow package로 저장해야 한다. 포함 요소는 입력 계약, 허용 도구, 금지 액션, 검증 명령, 실패 시 중단 기준, 보고 형식이다.
- workflow 플랫폼과 결합할 때는 deterministic node/API를 우선하고, LLM agent는 예외 처리·요약·계획·분류·초안·코드 생성처럼 비정형성이 필요한 구간에 배치하는 편이 안정적이다.
- 운영 지표는 “사용량”이 아니라 PR merge/time-to-merge, 재작업률, QA 발견 결함, false positive, draft acceptance, workflow failure, 권한 escalations, 비용/세션을 추적해야 한다.

## 인접 질문

- 조직의 반복 업무 중 “초안/패치/리포트/검증 로그”로 안전하게 분해 가능한 상위 20개 workflow는 무엇인가?
- 코딩 에이전트와 low-code workflow tool을 결합할 때, 어떤 작업은 deterministic automation으로 고정하고 어떤 작업만 agent autonomy로 남겨야 하는가?

## 출처 목록

| # | 출처 | 날짜/버전 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| 1 | OpenAI Codex web | 2026-04-22 확인 | 높음 | https://developers.openai.com/codex/cloud |
| 2 | OpenAI Codex use cases | 2026-04-22 확인 | 높음 | https://developers.openai.com/codex/use-cases |
| 3 | OpenAI Codex Workflows | 2026-04-22 확인 | 높음 | https://developers.openai.com/codex/workflows |
| 4 | OpenAI Codex Agent Skills | 2026-04-22 확인 | 높음 | https://developers.openai.com/codex/skills |
| 5 | OpenAI Codex Computer Use | 2026-04-22 확인 | 높음 | https://developers.openai.com/codex/app/computer-use |
| 6 | OpenAI Codex Generate slide decks use case | 2026-04-22 확인 | 높음 | https://developers.openai.com/codex/use-cases/generate-slide-decks |
| 7 | OpenAI Codex QA with Computer Use use case | 2026-04-22 확인 | 높음 | https://developers.openai.com/codex/use-cases/qa-your-app-with-computer-use |
| 8 | OpenAI Codex Manage your inbox use case | 2026-04-22 확인 | 높음 | https://developers.openai.com/codex/use-cases/manage-your-inbox |
| 9 | OpenAI Agents SDK | 2026-04-22 확인 | 높음 | https://developers.openai.com/api/docs/guides/agents |
| 10 | OpenAI Agent Builder | 2026-04-22 확인 | 높음 | https://developers.openai.com/api/docs/guides/agent-builder |
| 11 | Anthropic Claude Code common workflows | 2026-04-22 확인 | 높음 | https://code.claude.com/docs/en/tutorials |
| 12 | Anthropic Claude Code GitHub Actions | 2026-04-22 확인 | 높음 | https://code.claude.com/docs/en/github-actions |
| 13 | GitHub Docs: Copilot cloud agent | 2026-04-22 확인 | 높음 | https://docs.github.com/en/copilot/concepts/agents/cloud-agent/about-cloud-agent |
| 14 | GitHub Blog: assigning and completing issues with coding agent | 2025-06-06 | 중상 | https://github.blog/ai-and-ml/github-copilot/assigning-and-completing-issues-with-coding-agent-in-github-copilot/ |
| 15 | GitHub Agentic Workflows: Assign to Copilot | 2026-04-22 확인 | 높음 | https://github.github.com/gh-aw/reference/assign-to-copilot/ |
| 16 | Zapier Agents documentation | Updated 2026-03-31 | 높음 | https://help.zapier.com/hc/en-us/articles/24393442652557-Build-an-agent-in-Zapier-Agents |
| 17 | Zapier AI Actions | 2026-04-22 확인 | 중상 | https://actions.zapier.com/docs/platform/zapier/ |
| 18 | n8n AI Agent Tool node | 2026-04-22 확인 | 높음 | https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolaiagent/ |
| 19 | Microsoft Power Automate generative actions | Last updated 2026-01-16 | 높음 | https://learn.microsoft.com/en-us/power-automate/generative-actions-overview |
| 20 | Anthropic customer: Block + Claude in Databricks | 2026-04-22 확인 | 중상 | https://www.anthropic.com/customers/block |
| 21 | Anthropic customer: Graphite + Claude | 2026-04-22 확인 | 중상 | https://www.anthropic.com/customers/graphite |
| 22 | Anthropic customer: CodeRabbit + Claude | 2026-04-22 확인 | 중상 | https://www.anthropic.com/customers/coderabbit |
| 23 | OpenAI Codex product page | 2026-04-22 확인 | 중상 | https://openai.com/codex |
| 24 | NIST AI RMF Generative AI Profile | 2024 | 높음 | https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence |
| 25 | OWASP Top 10 for LLM Applications 2025 PDF | 2025 | 높음 | https://owasp.org/www-project-top-10-for-large-language-model-applications/assets/PDF/OWASP-Top-10-for-LLMs-v2025.pdf |
| 26 | OWASP Top 10 for Agentic Applications announcement | 2025-12-09 | 중상 | https://genai.owasp.org/2025/12/09/owasp-top-10-for-agentic-applications-the-benchmark-for-agentic-security-in-the-age-of-autonomous-ai/ |
| 27 | Comparing AI Coding Agents: A Task-Stratified Analysis of Pull Request Acceptance | arXiv 2602.08915, 2026 | 중상 | https://arxiv.org/abs/2602.08915 |
| 28 | Where Do AI Coding Agents Fail? | arXiv 2601.15195, 2026 | 중상 | https://arxiv.org/abs/2601.15195 |
| 29 | Reliability of AI Bots Footprints in GitHub Actions CI/CD Workflows | arXiv 2604.18334, 2026 | 중상 | https://arxiv.org/abs/2604.18334 |
| 30 | On the Use of Agentic Coding | arXiv 2509.14745, 2025 | 중상 | https://arxiv.org/abs/2509.14745 |
| 31 | AIDev: Studying AI Coding Agents on GitHub | arXiv 2602.09185, 2026 | 중상 | https://arxiv.org/abs/2602.09185 |
| 32 | A Survey on Autonomy-Induced Security Risks in Large Model-Based Agents | arXiv 2506.23844, 2025 | 중상 | https://arxiv.org/abs/2506.23844 |
| 33 | Agentic AI Risk-Management Standards Profile, CLTC | 2026 | 중상 | https://cltc.berkeley.edu/publication/agentic-ai-risk-profile/ |
| 34 | GitHub Copilot/Claude Code community failure discussions | 2025-2026 | 낮음 | https://www.reddit.com/r/GithubCopilot/ / https://www.reddit.com/r/ClaudeCode/ |
| 35 | n8n community AI Agent limitation discussions | 2025-2026 | 낮음 | https://www.reddit.com/r/n8n/ |

## 검색 포화 판단

공식 제품 문서 게이트는 OpenAI Codex/Agents, Anthropic Claude Code, GitHub Copilot, Zapier/n8n/Power Automate/GitHub Agentic Workflows로 충족했다. 직접 workflow 사례는 Block, Graphite, CodeRabbit, GitHub Copilot issue-to-PR, Codex use-case recipes로 3개 이상 확보했다. 반례/한계 검색은 지정 negative targets 전체를 수행했고, 공식 한계 문서와 OWASP/NIST/학술 실패 연구 및 커뮤니티 실패 사례를 교차 확인했다. 표준/학술/보고서 게이트는 NIST, OWASP, CLTC, arXiv agentic PR/CI/autonomy 연구로 충족했다.

더 검색해도 새로운 증거 유형보다는 특정 벤더별 최신 기능/가격/정책 업데이트가 늘어날 가능성이 높다. 아직 부족한 항목은 일반 업무 산출물(슬라이드, 이메일, 스프레드시트, 브라우저 업무)에 대한 독립 대규모 성과 데이터다. 다음 라운드에서는 특정 조직 내부 로그나 공개 benchmark가 있는지, 그리고 “draft-only 자동화”와 “full action 자동화”의 사고율 차이를 비교하는 자료를 찾아야 한다.
