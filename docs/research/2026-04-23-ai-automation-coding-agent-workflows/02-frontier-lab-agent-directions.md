# 프런티어 랩 에이전트 방향 - Codex/Claude Code 기반 업무 혁신 설계

**Researcher**: R2  
**Mode**: web  
**Date**: 2026-04-23  
**Scope**: OpenAI Codex/Agents/API, Anthropic Claude Code/Claude for Work, Google Gemini/Workspace/Agentspace/Gemini Code Assist/Antigravity/Jules의 공식 발표, 문서, 공개 고객 사례, 벤치마크와 한계를 조사한다. 공개된 내부 사용 사례는 포함하되, 추정은 분리한다. 최종 synthesis가 아니라 R2 관점의 bounded Researcher 산출물이다.

## 핵심 요약

- **결론**: 세 회사 모두 2025-2026년에 “채팅형 보조”에서 “도구·파일·브라우저·터미널을 쓰는 감독형 에이전트”로 제품 방향을 옮겼다. OpenAI는 Codex 앱/SDK/Responses API/Skills/Computer Use를, Anthropic은 Claude Code/Agent SDK/Claude for Work Integrations를, Google은 Gemini Enterprise/Code Assist agent mode/Gemini CLI/Antigravity를 전면에 둔다.
- **적용 조건**: Codex/Claude Code 기반 업무 혁신은 완전자율 실행보다 “검토 가능한 산출물, 권한 경계, 샌드박스, 로그, 평가 루프”를 먼저 설계할 때 맞다. 세 벤더 문서 모두 파일 수정, 명령 실행, 외부 앱 접근에 승인·격리·거버넌스를 붙인다.
- **공개 사례**: OpenAI는 내부에서 거의 모든 엔지니어가 Codex를 쓰고 PR을 더 많이 병합한다고 공개했다. Anthropic은 내부 설문/사용 로그와 법무팀 사례를 공개했고, 고객 사례로 Stripe/Ramp/Wiz/Rakuten/Zapier를 제시한다. Google은 Gemini Enterprise 고객·파트너 생태계와 Morrisons, Gemini Code Assist/DORA 기반 방향을 제시하지만, 최신 “Google 내부 업무 방식” 공개는 상대적으로 약하다.
- **가장 큰 한계**: 공식 벤치마크는 벤더별 측정 단위와 조건이 다르다. 독립 head-to-head는 일부 코딩 에이전트 PR 데이터와 APEX-Agents 같은 업무 에이전트 벤치마크가 있으나, OpenAI Codex, Claude Code, Google Antigravity/Jules/Gemini Code Assist를 같은 조건에서 모두 비교한 강한 직접증거는 아직 부족하다.
- **지금 설계에 반영할 점**: 업무 자동화는 “에이전트가 직접 완료”가 아니라 “에이전트가 초안/패치/리포트/테스트 결과를 만들고 사람이 승인”하는 운영 모델로 시작해야 한다. 보안상 기본값은 read-only, sandboxed, draft-only, restricted tools, audit logs가 되어야 한다.

## 읽는 법

이 문서는 Codex/Claude Code 기반 업무 혁신 설계에서 “프런티어 랩이 어디로 가는가”를 판단하기 위한 근거 묶음이다. 제품 기능 비교표가 아니라, 각 회사가 공개적으로 밀고 있는 업무 단위, 안전 장치, 고객 사례, 벤치마크 신호를 읽어 실제 조직 설계에 연결한다. 수치와 사례는 출처 유형이 섞여 있으므로, 벤더 발표 수치는 방향성 근거로 쓰고 독립 검증 수치는 제한적으로 해석한다.

## 주요 발견

### 1. OpenAI는 Codex를 “코딩 도구”에서 “컴퓨터로 일을 끝내는 에이전트 운영체계”로 확장하고 있다

OpenAI의 2025-2026년 흐름은 명확하다. 2025년 3월 Responses API와 Agents SDK로 에이전트 앱 개발 표면을 만들고, 2025년 5월 Codex research preview를 공개한 뒤, 2025년 10월 Codex GA에서 Slack, SDK, admin tooling을 붙였다. 2026년 2월 Codex 앱, 2026년 4월 “Codex for almost everything” 업데이트는 desktop/browser/computer use/plugins/memory/automations로 범위를 넓혔다.

업무 혁신 설계의 의미는 Codex를 IDE 안 보조도구로만 보지 말아야 한다는 점이다. Codex는 PR, CI, Slack, 파일, 브라우저, 데스크톱 앱, 반복 자동화, skills를 하나의 작업면으로 묶는 방향이다. 다만 OpenAI 스스로도 샌드박스, 기본 네트워크 차단, workspace 쓰기 제한, 관리자 통제를 강조하므로 “권한 있는 로컬/클라우드 작업자”로 설계해야 한다.

| 항목 | 공개 근거 | 판단 | 설계 의미 |
| --- | --- | --- | --- |
| Responses API/Agents SDK | 2025-03-11 OpenAI 발표: Responses API가 web search, file search, computer use, tracing/evals를 지원하고 Agents SDK가 multi-agent workflows를 오케스트레이션 | Fact | 업무 자동화 플랫폼은 API tool use와 평가/trace를 기본 계층으로 둬야 한다 |
| Codex 초기 방향 | 2025-05 Codex 발표: cloud agent는 격리 컨테이너, 인터넷 비활성, 반복·well-scoped 작업, 테스트/리팩터링/문서화에 사용 | Fact | 초도 업무는 범위가 명확하고 repo/context가 제한된 작업부터 시작 |
| Codex GA | 2025-10-06 GA: Slack integration, Codex SDK, admin tools, GitHub Action, 내부 OpenAI 엔지니어 사용과 PR 수치 공개 | Fact/Claim | Slack/PR/CI를 에이전트 요청·검토 큐로 삼는 구조가 맞다. 수치는 vendor-reported |
| 2026 Codex app | 2026-02-02 앱: 여러 에이전트를 동시에 관리, 장기 작업 협업, Automations로 issue triage/CI failure summary/release brief/bug checking 공개 | Fact/Claim | 반복 업무는 “프롬프트”가 아니라 automations/skills/workflow로 패키징해야 한다 |
| 2026 Codex 확장 | 2026-04-16: background computer use, in-app browser, image generation, 90+ plugins, memory/context-aware suggestions | Fact | 개발뿐 아니라 PM/QA/문서/디자인/운영 업무까지 파일·앱 기반 자동화 후보가 된다 |
| 보안 경계 | GPT-5.2-Codex system card: cloud isolated container, network disabled by default, local sandbox, workspace write restriction | Fact | 기본 정책은 network off, workspace 제한, domain allowlist, unsandboxed approval |

### 2. Anthropic은 Claude Code를 조직 전체의 “에이전트 오케스트레이션 습관”으로 설명한다

Anthropic은 Claude Code를 autocomplete가 아니라 프로젝트 단위 agentic coding system으로 정의한다. 공식 제품 설명은 full codebase 읽기, 계획, 파일 수정, 테스트, CI 실패 대응, GitHub/GitLab workflow를 강조한다. 동시에 보안 문서에서는 read-only 기본값, 명령 승인, sandboxed bash, prompt injection 대비, MCP 서버 신뢰 문제, cloud VM 격리를 명시한다.

특히 Anthropic은 내부 사용 방식을 많이 공개했다. 2025년 8월 132명 설문, 53명 인터뷰, Claude Code usage data를 분석해 “대부분 직원은 Claude를 자주 쓰지만 완전 위임 가능한 업무는 0-20%라고 보고한다”고 밝혔다. 이 점은 Codex/Claude Code 기반 혁신 설계에서 “사람이 감독하는 병렬 에이전트”가 현재 공개 근거에 가장 맞는 운영 모델임을 시사한다.

| 항목 | 공개 근거 | 판단 | 설계 의미 |
| --- | --- | --- | --- |
| Claude Code 방향 | 제품 페이지: project-level agent, test/CI loop, committed code, regulated/large codebase 고객 사례 | Fact/Claim | 엔지니어링 업무는 task delegation과 review 중심으로 재편 가능 |
| 내부 사용 분석 | 2025년 8월 설문 132명, 인터뷰 53명, usage data. 완전 위임 0-20%, 감독/검증 필요, feature 구현 비중 14.3%→36.9% | Fact/Claim | 성숙한 조직도 “full autopilot”보다 active supervision을 전제 |
| Agent SDK | Claude Agent SDK: Claude Code의 tools, agent loop, context management를 Python/TypeScript로 사용, 파일/명령/web search/edit/MCP/permissions/sessions 제공 | Fact | 사내 특화 업무 에이전트는 Claude Code 자체가 아니라 SDK 기반으로도 구성 가능 |
| Claude for Work | Enterprise/Integrations: Google Workspace, GitHub, Jira/Confluence, Zapier, MCP, Research, Artifacts, admin/security | Fact | knowledge work 자동화는 company context 연결과 citations/review가 핵심 |
| 고객 사례 | Stripe 1,370명 배포, Ramp incident investigation 80% 감소, Wiz 50,000-line migration 20 active hours, Rakuten delivery 24→5일, Zapier 800+ internal agents | Claim | 직접 사례로 유용하나 vendor/customer-reported라 효과 크기는 독립 검증 필요 |
| 내부 비개발 사례 | Anthropic legal team: Claude Code로 legal queue triage, G Suite apps, weekly updates, accessibility prototype 구축. “첫 시도 성공 약 1/3” 같은 한계도 공개 | Fact/Claim | 비개발 부서도 prototype/workflow tool을 만들 수 있으나 checkpoint-heavy 운영 필요 |
| 보안 | Claude Code security docs: read-only default, explicit permission, sandbox, blocklist, MCP server는 Anthropic이 audit하지 않음, no system immune | Fact | MCP와 prompt injection을 별도 threat model로 다뤄야 한다 |

### 3. Google은 Gemini를 Workspace/Cloud/Enterprise 전반의 agentic platform으로 묶고, 코딩 쪽은 Gemini CLI·Code Assist agent mode·Antigravity로 확장한다

Google의 방향은 “단일 코딩 에이전트”보다 Gemini Enterprise라는 전사 agentic platform이 중심이다. Google은 Agentspace가 Gemini Enterprise의 일부가 되었고, Workspace/Microsoft 365/Salesforce/SAP/Jira/Confluence 같은 회사 데이터 연결, no-code workbench, Agent Gallery, governance/audit를 강조한다. 코딩 쪽에서는 Gemini Code Assist agent mode, Gemini CLI, Google Antigravity, Jules가 병렬로 등장한다.

이 방향은 Codex/Claude Code 설계에 중요한 대비점을 준다. Google은 업무 데이터와 거버넌스의 엔터프라이즈 플랫폼을 앞세우고, coding agent는 그 안의 한 기능군으로 둔다. 반대로 Codex/Claude Code 기반 혁신은 개발자 도구에서 출발해 업무 산출물과 회사 앱으로 확장하는 접근이다.

| 항목 | 공개 근거 | 판단 | 설계 의미 |
| --- | --- | --- | --- |
| Gemini Enterprise | 2025-10-09 발표: chat front door, no-code workbench, prebuilt agents, company data connections, central governance | Fact | 전사 확산에는 agent registry/governance/connectors가 필요 |
| Agentspace 전환 | 제품 FAQ: Google Agentspace는 Gemini Enterprise의 일부가 됨 | Fact | Google은 enterprise search/assistant/orchestration을 하나의 구매·운영면으로 통합 |
| Code Assist agent mode | Docs: Preview, VS Code/IntelliJ, MCP, multi-step tasks, design doc/issue/TODO 기반 생성, plan/tool approval | Fact | coding agent UX는 Codex/Claude와 유사하게 plan-approve-tool loop로 수렴 |
| Agent mode 한계 | Docs: Pre-GA “as is”, 일부 chat 기능 미지원, recitation/citations 비가용, 외부 IDE 밖 변경 undo 없음 | Fact | production 사용 전 sandbox/backup/approval 운영이 필수 |
| Gemini CLI | 2025-06 발표: open-source AI agent, terminal에서 coding/problem solving/deep research/task management, 1M token context, free quota | Fact/Claim | CLI 기반 사내 agent workflow와 Code Assist가 같은 기술 기반으로 연결 |
| Antigravity | 2025-11-18 Gemini 3 발표: agent-first development platform, editor/terminal/browser access, simultaneous end-to-end tasks, browser computer use validation | Fact/Claim | Google도 “IDE가 아니라 agent workspace” 방향으로 이동 |
| Google 내부 사용 | 2024 Next 발표: Google 내부 개발자 그룹에서 common dev tasks 40%+ faster, new code writing time 55% less | Claim, older | 최신 2025-2026 내부 공개 사례는 제한적이다. 최신 방향 근거로 쓰기엔 약함 |
| 고객 사례 | Morrisons: Gemini/BigQuery/Looker로 Product Finder, customer feedback summarization, 개인 assistant 확장 검토 | Direct case | 업무 데이터 기반 assistant/agent 후보 발굴에는 강한 사례이나 coding agent 사례는 아님 |

### 4. 세 회사의 공개 방향은 “에이전트가 할 일”보다 “어떤 권한과 검증으로 일하게 할지”에서 갈린다

제품 표면은 모두 비슷해지고 있다. 파일을 읽고, 명령을 실행하고, 코드를 수정하고, 테스트를 돌리고, 브라우저나 앱을 조작한다. 실제 차이는 운영 기본값이다. OpenAI는 sandbox/network-off/admin controls, Anthropic은 permission prompts/sandbox/MCP caution, Google은 Pre-GA caveats/approval/tool configuration/enterprise governance를 앞세운다.

따라서 Codex/Claude Code 기반 업무 혁신 설계는 모델 선택보다 운영 경계가 먼저다. 업무마다 “에이전트가 읽을 수 있는 것, 쓸 수 있는 것, 실행할 수 있는 것, 승인 없이 할 수 있는 것, 실패하면 멈추는 조건”을 명시해야 한다.

| 설계 축 | OpenAI | Anthropic | Google | R2 판단 |
| --- | --- | --- | --- | --- |
| 핵심 표면 | Codex app/CLI/IDE/cloud, Responses API, Agents SDK, Skills, Plugins | Claude Code, Claude Agent SDK, Claude for Work, Integrations/MCP, Research | Gemini Enterprise, Code Assist agent mode, Gemini CLI, Antigravity, Jules | 모두 “agent workspace + tools”로 수렴 |
| 업무 확장 | Computer Use, browser, Slack/Gmail/Notion plugins, automations, skills | Claude for Work integrations, Zapier MCP, legal/marketing/research workflows | Enterprise connectors, no-code agent builder, Agent Gallery, Workspace/Cloud integration | 업무 혁신은 개발자 도구와 전사 플랫폼의 결합 문제 |
| 내부 사용 공개 | 거의 모든 OpenAI 엔지니어가 Codex 사용, 70% more PRs/week, almost every PR review | 설문/인터뷰/usage data, 완전 위임 0-20%, 법무팀 workflow 공개 | 2024 내부 개발자 성과 수치 외 최신 상세 공개 부족 | Anthropic이 내부 사용의 한계까지 가장 자세히 공개 |
| 보안 기본값 | isolated cloud, network disabled default, local sandbox, workspace write limits | read-only default, explicit permissions, sandboxed bash, MCP caution | Pre-GA, tool approval, core/exclude tools, enterprise access controls | 모든 설계는 least privilege와 audit를 기본값으로 해야 함 |
| 벤치마크 | SWE-Bench Pro, Terminal-Bench, OSWorld, GDPval 등 벤더 발표 | 고객 수치와 내부 usage, 일부 security/eval 자료 | SWE-bench Verified, Terminal-Bench 2.0, WebDev Arena 등 벤더 발표 | 벤더 벤치마크는 비교 단위가 달라 직접 순위화 금지 |

### 5. 독립 비교와 평가 근거는 아직 제한적이며, “업무 혁신”에는 코딩 벤치마크만으로 부족하다

독립 근거는 두 갈래다. 하나는 TechCrunch 같은 보도가 제품 경쟁 구도를 설명하는 자료이고, 다른 하나는 arXiv 등에서 PR acceptance, cross-application work benchmark, prompt injection, permission gate를 평가하는 자료다. 이 중 직접 비교에 가까운 것은 2026년 MSR Mining Challenge 논문으로 OpenAI Codex와 Claude Code를 포함한 5개 coding agent의 7,156개 PR acceptance를 비교했다.

그러나 Google Antigravity/Jules/Gemini Code Assist까지 같은 조건에서 비교한 공개 독립 자료는 약하다. APEX-Agents는 GPT/Claude/Gemini 계열 모델을 long-horizon cross-application tasks에서 비교하지만, Codex/Claude Code/Antigravity 같은 제품별 agent harness 직접 비교는 아니다. 따라서 “어떤 회사 제품이 우월하다”는 결론보다 “어떤 작업 유형과 운영 경계에서 성능을 직접 측정할 것인가”가 더 실무적이다.

| 근거 | 대상 | 핵심 결과 | 한계 | 설계 반영 |
| --- | --- | --- | --- | --- |
| TechCrunch, 2026-04-16 | OpenAI Codex vs Anthropic 경쟁 구도 | Codex desktop/browser/plugins가 Claude Code 계열 기능과 경쟁한다고 분석 | 보도/해석이며 성능 검증 아님 | 시장 방향은 coding→desktop/workplace 확장 |
| TechCrunch, 2025-10-20 | Claude Code web | Claude Code가 CLI를 넘어 web/mobile로 확장, agentic coding 경쟁 격화 | Anthropic 제공 수치 인용 포함 | 개발자는 agent operator/manager 역할로 이동 |
| Comparing AI Coding Agents, 2026-02 | Codex, Claude Code, Copilot, Devin, Cursor PR acceptance | task type이 acceptance에 큰 영향. Codex는 범주 전반 높고 Claude Code는 docs/features 강점 | Google coding agents 미포함, PR acceptance만 측정 | 사내 평가는 task-stratified로 해야 함 |
| APEX-Agents, 2026-01/02 | GPT/Claude/Gemini 모델 기반 업무 에이전트 | long-horizon cross-application tasks에서 최고 점수도 24% 수준 | 제품별 Codex/Claude Code/Antigravity 직접 비교 아님 | 실제 업무 자동화는 아직 낮은 완전완료율을 전제 |
| VPI-Bench, 2025/2026 | Computer-use/browser-use agents 보안 | 시각적 prompt injection이 CUA/BUA를 속일 수 있고 system prompt 방어가 제한적 | 특정 benchmark 환경 | 브라우저/desktop agent는 화면 내용 자체를 untrusted input으로 봐야 함 |
| Claude Code Auto Mode stress test, 2026-04 | Claude Code auto mode permission gate | ambiguous DevOps workload에서 false negative가 높게 나타남 | Claude Code 특정 기능, arXiv preprint | 자동 승인 모드는 scope/file-edit gap을 별도 통제해야 함 |

## 근거 표

주요 주장은 `Fact`(공식 문서·직접 데이터에 가까움), `Claim`(벤더/고객 발표 수치라 독립 검증 제한), `Unverified`(약한 보조 신호)로 나눴다. 같은 수치라도 제품 출시일·기능 존재는 Fact, 효과 크기는 Claim으로 해석했다.

| 주장 | 근거 | 출처 유형 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| OpenAI는 2025년 Responses API와 Agents SDK를 에이전트 앱 개발의 중심 API로 제시했다 | Responses API가 built-in tools, tracing/evals, multi-tool model turns를 지원한다고 발표 | official / Fact | 높음 | https://openai.com/index/new-tools-for-building-agents/ |
| Codex는 2025년 research preview에서 격리 cloud agent로 시작했고, well-scoped engineering tasks를 대상으로 했다 | Codex cloud agent, secure container, no internet during task execution, refactoring/testing/docs use cases | official / Fact | 높음 | https://openai.com/index/introducing-codex/ |
| OpenAI는 2025년 10월 Codex GA에서 Slack, SDK, admin tools, internal engineering adoption을 공개했다 | GA 발표가 Slack, SDK, admin controls, almost all engineers, 70% more PRs를 제시 | official / Fact/Claim | 중상 | https://openai.com/index/codex-now-generally-available/ |
| OpenAI는 2026년 4월 Codex를 desktop/browser/plugin/memory/automation으로 확장했다 | background computer use, in-app browser, image generation, 90+ plugins, automations | official / Fact | 높음 | https://openai.com/index/codex-for-almost-everything/ |
| Codex 보안 모델은 sandbox와 network-off default가 핵심이다 | GPT-5.2-Codex system card가 cloud isolated container, network disabled, local sandbox, workspace write restriction을 설명 | official / Fact | 높음 | https://cdn.openai.com/pdf/ac7c37ae-7f4c-4442-b741-2eabdeaf77e0/oai_5_2_Codex.pdf |
| Anthropic은 Claude Code를 project-level agentic coding system으로 정의한다 | 제품 페이지가 codebase read/plan/execute/test/commit, CI failures, toolchain execution을 설명 | official / Fact | 높음 | https://www.anthropic.com/product/claude-code |
| Anthropic 내부 사용 공개는 감독형 위임 모델을 지지한다 | 132명 설문, 53명 인터뷰, usage data. 완전 위임 0-20%, 감독/검증 필요 | official / Fact/Claim | 중상 | https://www.anthropic.com/news/how-ai-is-transforming-work-at-anthropic |
| Claude Agent SDK는 Claude Code의 agent harness를 제품 내장 에이전트로 재사용하게 한다 | SDK docs가 files/commands/web search/edit/MCP/permissions/sessions를 설명 | official / Fact | 높음 | https://code.claude.com/docs/en/agent-sdk/overview |
| Claude Code는 보수적인 permission architecture와 prompt injection 방어를 문서화한다 | read-only default, explicit permission, sandbox, command blocklist, MCP trust caution, cloud VM controls | official / Fact | 높음 | https://code.claude.com/docs/en/security |
| Claude for Work/Enterprise는 company knowledge, GitHub, Google Workspace, integrations, audit/security를 업무 표면으로 둔다 | Enterprise and integrations pages | official / Fact | 높음 | https://claude.com/pricing/enterprise / https://claude.com/blog/integrations |
| Zapier는 Claude/Claude Code를 전사 workflow와 engineering automation에 쓴다고 공개했다 | 89% adoption, 800+ internal agents, Slack emoji→MR workflow 등 | direct case / Claim | 중상 | https://claude.com/customers/zapier |
| Google은 Agentspace를 Gemini Enterprise로 통합하고 agentic platform으로 포지셔닝한다 | Gemini Enterprise product FAQ와 docs가 Agentspace 전환, connectors, agent gallery, governance를 설명 | official / Fact | 높음 | https://cloud.google.com/gemini-enterprise / https://docs.cloud.google.com/gemini/enterprise/docs |
| Gemini Code Assist agent mode는 plan/tool approval 방식의 coding agent다 | Preview docs: MCP, multi-step tasks, file/terminal tools, permission checks, plan approval | official / Fact | 높음 | https://docs.cloud.google.com/gemini/docs/codeassist/agent-mode |
| Gemini Code Assist agent mode는 아직 Pre-GA이고 일부 한계가 명시되어 있다 | Pre-GA “as is”, recitation/citations unavailable, outside-IDE undo caution | official / Fact | 높음 | https://docs.cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer |
| Google은 Gemini 3와 Antigravity를 agent-first development experience로 발표했다 | 2025-11-18 발표: editor/terminal/browser access, autonomous end-to-end tasks, validation | official / Fact/Claim | 중상 | https://blog.google/products-and-platforms/products/gemini/gemini-3/ |
| Gemini CLI는 terminal agent이자 Code Assist와 연결되는 개발자 표면이다 | 2025년 발표: open-source AI agent, coding/problem solving/deep research/task management, 1M context, quotas | official / Fact/Claim | 중상 | https://blog.google/innovation-and-ai/technology/developers-tools/introducing-gemini-cli-open-source-ai-agent/ |
| Morrisons 사례는 Gemini/BigQuery/Looker 기반 업무 데이터 assistant 방향을 보여준다 | Product Finder, customer feedback summarization, personal assistants 검토 | direct case / Claim | 중상 | https://cloud.google.com/customers/morrisons |
| 독립 보도는 Codex와 Claude Code 경쟁이 coding에서 desktop/workplace로 확장됨을 지적한다 | TechCrunch 2026-04-16, 2025-10-20 | reliable / Claim | 중간 | https://techcrunch.com/2026/04/16/openai-takes-aim-at-anthropic-with-beefed-up-codex-that-gives-it-more-power-over-your-desktop/ |
| PR acceptance 독립 비교는 작업 유형별 차이가 agent 간 차이만큼 중요함을 보여준다 | 7,156 PR, Codex/Claude Code 포함 5개 agent, task-stratified analysis | academic / Claim | 중상 | https://arxiv.org/abs/2602.08915 |
| cross-application 업무 에이전트는 아직 완전 자동화 성공률이 낮다 | APEX-Agents에서 최고 Pass@1 24.0% | academic / Claim | 중상 | https://arxiv.org/abs/2601.14242 |
| computer-use/browser-use agents는 시각적 prompt injection에 취약할 수 있다 | VPI-Bench 306 cases, 특정 조건에서 높은 deception rates | academic / Claim | 중상 | https://arxiv.org/abs/2506.02456 |
| Claude Code auto mode 같은 permission gate도 ambiguous tasks에서 coverage gap이 생길 수 있다 | 2026-04 arXiv stress test가 high FNR과 Tier 2 file-edit gap을 보고 | academic / Claim | 중간 | https://arxiv.org/abs/2604.04978 |

## 출처 품질 매트릭스

공식 출처 수는 충분하지만, 성과 수치 대부분은 벤더/고객 발표다. 독립 출처는 제품 경쟁 구도와 일부 평가·보안 문제를 보강하지만, 세 회사 제품을 같은 조건에서 직접 비교하는 증거는 아직 제한적이다.

| 출처 유형 | 개수 | 핵심 기여 | 약점 |
| --- | ---: | --- | --- |
| official / primary | 17 | OpenAI, Anthropic, Google 각각의 최신 제품 방향, 기능, 보안 기본값, 공개 내부 사용 확인 | 벤더 발표는 성공 사례와 유리한 벤치마크를 강조 |
| official direct case | 4 | OpenAI internal, Anthropic internal/legal, Zapier, Morrisons 등 실제 사용 단서 | 효과 수치가 독립 감사된 것은 아님 |
| independent reporting / analysis | 2 | TechCrunch가 Codex/Claude Code 경쟁, Claude Code web 확장, 시장 구도 설명 | 성능 검증보다는 보도와 해석 |
| academic / benchmark | 4 | PR acceptance 비교, APEX 업무 벤치마크, VPI-Bench, permission gate stress test | arXiv/preprint 비중이 있고 일부는 제품 직접 비교가 아님 |
| security / limitation docs | 5 | Codex system card, Claude security docs, Google agent mode limitations, VPI, Auto Mode stress test | 실제 조직별 사고율·운영비 데이터는 부족 |
| weak / unverified | 0 | 핵심 주장에는 미사용 | 커뮤니티 루머/약한 블로그는 배제 |

## 반례/실패 사례 검색 로그

반례 검색은 “기능이 된다”보다 “어디서 멈춰야 하는가”를 찾는 데 집중했다. 결과는 권한, 샌드박스, prompt injection, benchmark contamination, task mismatch로 모인다.

| 쿼리 | 목적 | 결과 | 결론 영향 |
| --- | --- | --- | --- |
| `OpenAI Codex limitations security sandbox network disabled` | Codex 한계와 보안 기본값 확인 | Codex 초기 발표와 GPT-5.2-Codex system card에서 network disabled, sandbox, workspace restriction 확인 | Codex 자동화는 network/domain allowlist와 workspace 제한을 기본값으로 둬야 함 |
| `Claude Code security prompt injection permissions sandbox MCP` | Claude Code permission/MCP 위험 확인 | 공식 security docs가 read-only default, explicit permission, MCP 서버 미감사, no system immune 명시 | Claude Code 기반 설계는 MCP trust registry와 permission policy 필요 |
| `Gemini Code Assist agent mode limitations Preview undo outside IDE` | Google coding agent 한계 확인 | Pre-GA “as is”, recitation/citations unavailable, outside IDE changes no undo caution 확인 | Gemini agent mode는 production 전 backup/approval/scope 제한 필요 |
| `AI coding agents direct comparison Codex Claude Code Gemini` | 세 회사 직접 비교 확인 | Codex/Claude Code 포함 PR 비교 논문은 있으나 Google coding agent까지 포함한 강한 제품 직접 비교는 찾지 못함 | `비교 직접증거 없음`을 불확실성에 반영 |
| `coding agents failed pull requests benchmark limitations` | PR acceptance와 실패 조건 확인 | Comparing AI Coding Agents에서 task type 차이가 크게 작용 | 내부 평가는 task-stratified로 설계해야 함 |
| `cross application AI agents benchmark long horizon work limitations` | 업무 자동화 전체 성공률 확인 | APEX-Agents에서 최고 Pass@1 24.0% 수준 | 장기·다중 앱 업무는 full automation보다 draft/review 기반이 맞음 |
| `computer use agents prompt injection visual prompt injection benchmark` | 브라우저/desktop 에이전트 보안 반례 확인 | VPI-Bench가 visual prompt injection 취약성 제시 | 화면·웹페이지·문서 내용을 untrusted input으로 간주 |
| `Claude Code auto mode permission gate stress test` | 자동 승인 모드 위험 확인 | 2026-04 stress test가 ambiguous workload에서 high false negative와 file-edit coverage gap 보고 | 자동 승인은 shell만 아니라 file edit/side effect까지 통제해야 함 |
| `DORA generative AI software delivery throughput stability 2025` | AI coding adoption의 시스템 성과 반례 확인 | Google Cloud/DORA 요약에서 AI adoption 증가가 throughput/stability 개선으로 직결되지 않는다고 설명 | 생산성 설계는 개인 속도보다 system bottleneck과 품질 지표를 봐야 함 |

## 상충점과 불확실성

- **직접 비교 증거 없음**: OpenAI Codex, Anthropic Claude Code, Google Gemini Code Assist/Antigravity/Jules를 같은 harness, 같은 repo, 같은 업무 범위, 같은 비용 조건에서 비교한 강한 독립 직접증거를 찾지 못했다. Codex/Claude Code 등 일부 coding agent PR 비교와 GPT/Claude/Gemini 모델 기반 업무 benchmark는 있지만 제품 전체 비교로 일반화하면 안 된다.
- **벤더 수치의 독립 검증 한계**: OpenAI 내부 PR 70% 증가, Anthropic 고객의 migration/incident/delivery 수치, Google 내부/고객 생산성 수치는 모두 방향성은 강하지만 독립 감사나 대조군이 제한적이다.
- **Google 내부 최신 사용 공개 부족**: Google은 Gemini Enterprise와 Code Assist/Antigravity 방향을 잘 공개했지만, 2025-2026년에 Google 내부에서 coding/agent workflows를 어떻게 운영하는지에 대한 상세 공개는 OpenAI/Anthropic보다 적게 확인됐다. 2024 Next의 내부 개발자 수치는 역사적 참고로만 써야 한다.
- **벤치마크 단위 불일치**: SWE-bench, SWE-Bench Pro, Terminal-Bench, WebDev Arena, APEX-Agents, GDPval, OSWorld는 각각 측정 대상이 다르다. 서로 다른 점수를 “업무 자동화 성능 순위”로 합치면 안 된다.
- **보안 자료의 빠른 변동성**: 2026년 들어 desktop/browser/computer use, auto mode, plugin/MCP가 빠르게 바뀌고 있다. 보안 기본값, 제품 한계, pricing, rate limits는 도입 시점에 재확인해야 한다.
- **추정과 사실 분리**: “개발자 도구에서 일반 업무 자동화로 확장될 것”은 공식 제품 방향과 기능에서 강하게 추론되지만, 모든 부서에서 ROI가 난다는 직접증거는 아직 부족하다.

## 의사결정 영향

Codex/Claude Code 기반 업무 혁신 설계는 “어떤 모델을 고를까”보다 “어떤 업무를 어떤 권한으로 맡길까”를 먼저 정해야 한다. 공식·독립 근거를 종합하면 초도 적용은 PR/테스트/문서/QA/CI triage/리서치/보고서/데이터 검증/내부 도구 prototype처럼 검토 가능한 산출물이 남는 업무가 맞다.

조직 운영 모델은 다음 기준으로 설계하는 편이 안전하다. 첫째, 모든 workflow는 input contract, allowed tools, disallowed tools, approval gates, validation command, rollback path, audit log를 가진다. 둘째, 에이전트는 draft/patch/report를 만들고 사람은 merge/send/deploy/pay/delete 같은 최종 action을 승인한다. 셋째, 반복 업무는 skills/routines/automations/workflows로 패키징하고, 단발 prompt를 운영 자산으로 취급하지 않는다.

| 설계 결정 | 권고 | 근거 |
| --- | --- | --- |
| 초도 업무 | well-scoped repo tasks, docs, tests, CI failure summary, QA report, release notes, internal prototype | OpenAI/Anthropic/Google 모두 이 범위의 agent workflow를 공식화 |
| 업무 완료 정의 | “완료”보다 “리뷰 가능한 산출물+검증 로그” | Anthropic 내부 사용도 full delegation 0-20%, APEX 최고 24% |
| 보안 기본값 | read-only first, sandbox, network off, workspace write restriction, domain allowlist, explicit approval | Codex system card, Claude security, Gemini agent mode docs |
| 비개발 부서 확장 | 법무/마케팅/운영/데이터 업무는 prototype/draft/research/report부터 | Anthropic legal, Zapier, Google Gemini Enterprise/Morrisons |
| 평가 지표 | task type별 acceptance, rework, test pass, review findings, incident time, false positive/negative, approval escalations, cost/session | 독립 PR 비교와 DORA식 system-level measurement 필요 |
| 벤더 비교 | 공개 benchmark 순위 대신 사내 benchmark를 만든다 | 직접 head-to-head evidence 부족, benchmark 단위 불일치 |

## 인접 질문

- 우리 조직의 상위 20개 반복 업무 중 “초안/패치/리포트/검증 로그”로 남길 수 있고, 권한을 좁힐 수 있는 업무는 무엇인가?
- Codex/Claude Code를 직접 쓰는 업무와 Gemini Enterprise/Workspace 같은 전사 agent platform에 맡길 업무의 경계는 어디인가?

## 출처 목록

| # | 출처 | 날짜/버전 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| 1 | OpenAI, New tools for building agents | 2025-03-11 | 높음 | https://openai.com/index/new-tools-for-building-agents/ |
| 2 | OpenAI, Introducing Codex | 2025-05, 2026-04-23 확인 | 높음 | https://openai.com/index/introducing-codex/ |
| 3 | OpenAI, Introducing upgrades to Codex | 2025-09-15, 2025-09-23 update | 높음 | https://openai.com/index/introducing-upgrades-to-codex/ |
| 4 | OpenAI, Codex is now generally available | 2025-10-06 | 높음 | https://openai.com/index/codex-now-generally-available/ |
| 5 | OpenAI, Introducing the Codex app | 2026-02-02, 2026-03-04 update | 높음 | https://openai.com/index/introducing-the-codex-app/ |
| 6 | OpenAI, Introducing GPT-5.3-Codex | 2026-02-05 | 중상 | https://openai.com/index/introducing-gpt-5-3-codex/ |
| 7 | OpenAI, Codex for almost everything | 2026-04-16 | 높음 | https://openai.com/index/codex-for-almost-everything/ |
| 8 | OpenAI Developers, Codex Agent Skills | 2026-04-23 확인 | 높음 | https://developers.openai.com/codex/skills |
| 9 | OpenAI API Docs, Agents SDK | 2026-04-23 확인 | 높음 | https://developers.openai.com/api/docs/guides/agents |
| 10 | OpenAI, Addendum to GPT-5.2 System Card: GPT-5.2-Codex | 2025/2026 공개, 2026-04-23 확인 | 높음 | https://cdn.openai.com/pdf/ac7c37ae-7f4c-4442-b741-2eabdeaf77e0/oai_5_2_Codex.pdf |
| 11 | Anthropic, Claude Code product page | 2026-04-23 확인 | 높음 | https://www.anthropic.com/product/claude-code |
| 12 | Anthropic, How AI Is Transforming Work at Anthropic | 2025-12 전후 공개, 2026-04-23 확인 | 높음 | https://www.anthropic.com/news/how-ai-is-transforming-work-at-anthropic |
| 13 | Claude Code Docs, Claude Agent SDK overview | 2026-04-23 확인 | 높음 | https://code.claude.com/docs/en/agent-sdk/overview |
| 14 | Claude Code Docs, Security | 2026-04-23 확인 | 높음 | https://code.claude.com/docs/en/security |
| 15 | Anthropic, Claude can now connect to your world | 2025-05-01, 2025-06-03 update | 높음 | https://claude.com/blog/integrations |
| 16 | Anthropic, Claude Enterprise plan | 2026-04-23 확인 | 높음 | https://claude.com/pricing/enterprise |
| 17 | Anthropic, Zapier customer story | 2026-04-23 확인 | 중상 | https://claude.com/customers/zapier |
| 18 | Anthropic, 2026 Agentic Coding Trends Report | 2026 | 중상 | https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf?hsLang=en |
| 19 | Anthropic, How Anthropic teams use Claude Code PDF | 2025/2026, 2026-04-23 확인 | 중상 | https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf |
| 20 | Google Cloud, Introducing Gemini Enterprise | 2025-10-09 | 높음 | https://cloud.google.com/blog/products/ai-machine-learning/introducing-gemini-enterprise |
| 21 | Google Cloud, Gemini Enterprise product page | 2026-04-23 확인 | 높음 | https://cloud.google.com/gemini-enterprise |
| 22 | Google Cloud Docs, What is Gemini Enterprise? | Last updated 2025-10-24 | 높음 | https://docs.cloud.google.com/gemini/enterprise/docs |
| 23 | Google Cloud Docs, Gemini Code Assist agent mode overview | 2026-04-23 확인 | 높음 | https://docs.cloud.google.com/gemini/docs/codeassist/agent-mode |
| 24 | Google Cloud Docs, Use Gemini Code Assist agent mode | 2026-04-23 확인 | 높음 | https://docs.cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer |
| 25 | Google, Gemini 3 announcement | 2025-11-18 | 높음 | https://blog.google/products-and-platforms/products/gemini/gemini-3/ |
| 26 | Google Developers Blog, Gemini 3 for developers | 2025-11-18 | 높음 | https://blog.google/innovation-and-ai/technology/developers-tools/gemini-3-developers/ |
| 27 | Google Developers Blog, Gemini CLI open-source AI agent | 2025-06 | 높음 | https://blog.google/innovation-and-ai/technology/developers-tools/introducing-gemini-cli-open-source-ai-agent/ |
| 28 | Google Cloud Blog, Gemini Code Assist agents and DORA | 2025-05-14 | 중상 | https://cloud.google.com/blog/topics/developers-practitioners/read-doras-latest-research-on-software-excellence |
| 29 | Google Cloud, Morrisons case study | 2026-04-23 확인 | 중상 | https://cloud.google.com/customers/morrisons |
| 30 | TechCrunch, OpenAI takes aim at Anthropic with beefed-up Codex | 2026-04-16 | 중간 | https://techcrunch.com/2026/04/16/openai-takes-aim-at-anthropic-with-beefed-up-codex-that-gives-it-more-power-over-your-desktop/ |
| 31 | TechCrunch, Anthropic brings Claude Code to the web | 2025-10-20 | 중간 | https://techcrunch.com/2025/10/20/anthropic-brings-claude-code-to-the-web/ |
| 32 | Pinna et al., Comparing AI Coding Agents | arXiv 2602.08915, 2026-02-09 | 중상 | https://arxiv.org/abs/2602.08915 |
| 33 | Vidgen et al., APEX-Agents | arXiv 2601.14242, v3 2026-02-23 | 중상 | https://arxiv.org/abs/2601.14242 |
| 34 | Cao et al., VPI-Bench | arXiv 2506.02456, v2 2026-03-01 | 중상 | https://arxiv.org/abs/2506.02456 |
| 35 | Ji et al., Measuring the Permission Gate | arXiv 2604.04978, 2026-04-04 | 중간 | https://arxiv.org/abs/2604.04978 |

## 검색 포화 판단

필수 깊이 게이트는 충족했다. OpenAI, Anthropic, Google 각각 공식/1차 출처를 2개 이상 확보했고, 독립 보도/분석은 TechCrunch 2건과 독립 학술/벤치마크 자료를 추가로 확보했다. 코딩 에이전트의 한계/보안/평가 출처는 Codex system card, Claude security docs, Gemini Code Assist limitations docs, VPI-Bench, Claude Code Auto Mode stress test, PR acceptance 비교, APEX-Agents로 3개 이상 확보했다. 2025-2026 최신 변화는 날짜를 확인했다.

검색을 더 해도 새로운 증거 유형보다는 벤더별 세부 기능, 가격, 커뮤니티 반응, 약한 블로그 비교가 늘어날 가능성이 높다. 아직 부족한 항목은 세 회사 제품을 같은 조건에서 비교한 강한 head-to-head evidence와, Google 내부의 2025-2026 agent/coding workflow 상세 공개다. 다음 라운드가 있다면 사내 benchmark 설계용으로 동일 repo/동일 task/동일 권한 조건에서 Codex, Claude Code, Gemini Code Assist/Antigravity를 직접 실험하는 것이 검색보다 더 유효하다.
