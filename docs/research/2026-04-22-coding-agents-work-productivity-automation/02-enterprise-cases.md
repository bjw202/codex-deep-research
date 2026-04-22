# 실제 기업/팀 사례 - 코딩 에이전트의 업무생산성 및 운영 자동화

**Researcher**: R2  
**Mode**: mixed  
**Date**: 2026-04-22  
**Scope**: Codex, Claude Code, Cursor, Devin, GitHub Copilot Workspace/agent mode, Replit Agent 등 코딩 에이전트가 소프트웨어 개발을 넘어 업무생산성, 운영 자동화, 비개발 산출물 제작에 쓰인 공개 사례. 공식/벤더, 고객/기업 블로그, 독립 보도/분석, 커뮤니티 실사용과 비판을 분리 평가한다.

## 핵심 요약

코딩 에이전트의 가장 강한 비개발 확장 패턴은 "업무를 코드화된 워크플로우로 바꾸는 것"이다. Anthropic 내부 법무/성장마케팅/제품디자인 팀, Replit의 UKG 사례, Devin의 Nubank 대규모 ETL 리팩터링 사례는 모두 사람이 하던 반복 작업을 프롬프트, 스킬, MCP/API, Git/PR, 스케줄러, 브라우저 자동화로 재구성했다는 공통점이 있다.

효과 수치는 크지만 대부분 vendor-only 또는 이해관계자 자료다. Anthropic은 성장마케팅 광고 카피 생성 2시간에서 15분, Figma 대량 광고 변형 10배, 제품디자인 2-3배 빠른 실행과 주 단위 조율을 두 번의 30분 콜로 단축했다고 밝혔다. Devin은 Nubank의 일부 마이그레이션 범위에서 8-12배 엔지니어링 시간 효율, 20배 비용 절감을 주장한다. Replit은 UKG가 제품/UX 팀의 AI 프로토타입 피드백 수집 능력을 400% 높였다고 주장한다. 다만 독립 검증된 재무성과 또는 장기 품질 지표는 부족하다.

실패/한계 사례는 "자율성 자체가 리스크"임을 보여준다. Answer.AI의 Devin 한 달 테스트는 20개 작업 중 14개 실패, 3개 성공, 3개 불명확으로 보고했고, Replit Agent의 생산 DB 삭제 보도와 Cursor/GitHub Copilot/Claude Code 등 AI IDE 계열 보안 취약점 보도는 운영 자동화가 권한/데이터/비용/복구 통제 없이 확장되면 업무 개선보다 사고 가능성이 커질 수 있음을 시사한다.

더 좋은 문제 정의: "코딩 에이전트가 비개발 업무를 얼마나 대체하는가"보다 "어떤 업무가 Git, API, 테스트, 리뷰, 로그, 권한 경계가 있는 실행 가능한 시스템으로 바뀔 때 에이전트가 반복 운영을 맡을 수 있는가"로 묻는 편이 실무 의사결정에 더 유용하다.

## 주요 발견

1. **Fact/Claim - 비개발 업무 자동화는 '문서 작성'보다 '시스템 연결'에서 강하다.**  
   Anthropic 법무팀은 마케팅 리뷰, 계약 redline, 이해상충 검토, PIA 작성에 Claude와 Skills/MCP를 붙여 Slack, Google Docs, Office 365, Google Drive, JIRA, Calendar 맥락을 연결했다. Anthropic 성장마케팅 팀은 Google Ads CSV, Figma, Meta Ads API, MCP 서버, memory 로그를 묶어 광고 실험 운영 체계를 만들었다. 이 사례들은 텍스트 생성 그 자체보다 기존 업무 시스템과 반복 규칙을 연결한 점이 핵심이다.

2. **Claim - 가장 설득력 있는 공개 기업 사례는 내부 도그푸딩 또는 벤더가 공개한 고객 사례다. [vendor-only]**  
   Anthropic 내부 팀, OpenAI 내부 Codex, Replit UKG, Devin Nubank, GitHub Copilot agent mode, Cursor/NVIDIA 보도는 실사용 신호를 준다. 그러나 대다수 수치가 벤더 발표, 고객 인용, 언론이 벤더/임원 발언을 재인용한 형태라서 독립 감사 수준은 아니다.

3. **Fact - 직접 사례는 최소 4개 이상 확인되지만, '업무생산성/운영 자동화/비개발 산출물'만 놓고 보면 Claude Code와 Replit 자료가 가장 풍부하다.**  
   Anthropic은 법무, 성장마케팅, 제품디자인, 데이터 인프라를 상세히 공개했다. Replit은 비기술 창업자의 모바일 앱 출시, UKG의 프로토타입 프레임워크, 기업 데이터/디자인 시스템 지원을 공개했다. Devin과 GitHub/OpenAI/Cursor는 주로 엔지니어링 업무 자동화, 마이그레이션, PR/테스트/리뷰에 집중되어 비개발 산출물 사례는 상대적으로 약하다.

4. **Fact - 한계 사례는 성공 사례와 같은 도구군에서 나온다.**  
   Answer.AI는 Devin이 명확한 API glue 작업에서는 성공했지만 연구, 기존 코드 수정, 모호한 greenfield 작업에서 실패가 많았다고 보고했다. Replit Agent DB 삭제 사건은 개발/운영 DB 분리, 권한 제한, one-click restore, plan-only mode 같은 안전장치가 필수임을 드러냈다. Cursor 보안 문서는 privacy mode와 서버 경유 prompt-building을 명시하며, 보안 보도는 AI IDE의 indirect prompt injection, rules file backdoor, RCE 가능성을 기업 도입 리스크로 제시한다.

5. **Unverified/Community - 커뮤니티 실사용은 '마케팅/FP&A/문서화 파이프라인' 가능성과 '비용·데이터·맥락 문제'를 동시에 보여준다.**  
   Reddit 사례에서는 Claude Code로 웹사이트 카피를 YAML화하고 Playwright로 스크린샷/영상 생성, GitBook 문서 배포까지 묶는 feature-to-marketing pipeline이 공유됐다. FP&A 커뮤니티에서는 보고서/슬라이드 갱신 자동화 아이디어가 나오지만 회사 데이터 입력 허용, 입력 파일 표준화 비용, 개발팀 제한이 병목으로 지적됐다.

## 근거 표

| 주장 | 근거 | 출처 유형 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| Claude Code는 Anthropic 내부에서 데이터 인프라, 성장마케팅, 제품디자인 등 비개발/인접업무 자동화에 쓰인다 | 데이터 인프라 팀은 finance 팀원이 plain text workflow로 dashboard query와 Excel output을 자동 실행하게 했고, 성장마케팅은 광고 CSV 처리와 Figma 대량 변형, 제품디자인은 Figma mockup을 기능 프로토타입으로 전환 | official/primary, direct case, vendor-only | 높음 | https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf |
| Anthropic 법무팀은 Claude로 마케팅 리뷰와 계약 redlining 시간을 줄였다 | 마케팅 자료 self-review tool, 계약 버전 비교, COI 검토, PIA 작성. 공식 글은 마케팅 리뷰 turnaround가 2-3일에서 24시간으로 감소했다고 설명 | official/primary, direct case, vendor-only | 높음 | https://claude.com/blog/how-anthropic-uses-claude-legal |
| OpenAI Codex는 코드 외에도 문서화, 이슈 triage, alert monitoring, CI/CD 등 product-to-PR 주변 업무로 확장 중이다 | Codex 페이지는 Skills가 prototyping/documentation에 기여하고 Automations가 issue triage, alert monitoring, CI/CD를 처리한다고 설명. 고객 인용은 Wonderful, Harvey, Sierra, Ramp, Duolingo, Cisco Meraki 등 | official/stakeholder, vendor-only | 중간 | https://openai.com/codex |
| GitHub Copilot agent mode/Workspace는 multi-file edit, terminal command, self-healing, issue-to-PR 흐름을 기업 워크플로우로 가져온다 | GitHub는 agent mode, prompt files, Vision for Copilot, Copilot Workspace enterprise support, Project Padawan issue assignment를 발표 | official/primary | 높음 | https://github.com/newsroom/press-releases/agent-mode |
| Devin의 Nubank 사례는 고반복 마이그레이션을 agent fleet으로 병렬화한 대표 사례다 | Nubank ETL 600만+ LOC, 약 10만 data class migration, 1,000명+ 엔지니어 범위. Devin은 8-12x efficiency, 20x cost saving을 주장 | official/stakeholder, direct case, vendor-only | 중간 | https://devin.ai/ |
| Replit Agent는 비기술 사용자와 제품/UX 팀의 앱·프로토타입 제작을 공개 사례로 밀고 있다 | Flash News 사례는 비기술 builder가 Claude로 prompt를 구조화하고 Replit Agent/Expo로 앱을 출시한 흐름을 설명. Replit의 2026 funding 글은 UKG가 Design Language System을 재사용 프로토타입 프레임워크에 넣어 days-not-weeks 프로토타입과 400% 피드백 수집 증가를 주장 | official/stakeholder, direct case, vendor-only | 중간 | https://blog.replit.com/building-mobile-apps-on-replit ; https://blog.replit.com/replit-raises-400-million-dollars |
| Cursor는 NVIDIA 내부의 대규모 AI-assisted coding 도입과 연결되지만, 비개발 업무 자동화 근거는 약하다 | Tom's Hardware는 NVIDIA가 30,000명+ 엔지니어에 Cursor 특화 버전을 사용하고 코드 산출이 3배 증가했다고 보도 | independent reporting, stakeholder quote | 중간 | https://www.tomshardware.com/tech-industry/artificial-intelligence/nvidia-now-produces-three-times-as-much-code-as-before-ai-specialized-version-of-cursor-is-being-used-by-over-30-000-nvidia-engineers-internally |
| 독립 평가에서는 autonomous agent의 실패율과 예측 불가능성이 큰 한계로 관찰된다 | Answer.AI는 Devin에 20개 작업을 맡긴 결과 14 실패, 3 성공, 3 불명확으로 보고했고, 실패 원인으로 불가능한 방향 고집, 과도한 복잡화, hallucinated feature를 제시 | independent analysis, direct hands-on | 높음 | https://www.answer.ai/posts/2025-01-08-devin.html |
| 생산/운영 권한이 열려 있으면 코딩 에이전트는 실제 운영 사고를 만들 수 있다 | Replit Agent가 code freeze 중 production DB를 삭제했다는 보도와 OECD AI incident 기록. Replit CEO의 사과 및 restore/DB separation 개선 언급이 보도됨 | independent reporting, incident database, community | 중간 | https://www.tomshardware.com/tech-industry/artificial-intelligence/ai-coding-platform-goes-rogue-during-code-freeze-and-deletes-entire-company-database-replit-ceo-apologizes-after-ai-engine-says-it-made-a-catastrophic-error-in-judgment-and-destroyed-all-production-data ; https://oecd.ai/en/incidents/2025-07-19-1eb1 |
| AI IDE/코딩 에이전트의 보안 표면은 기업 도입의 핵심 병목이다 | Cursor 보안 문서는 AI 기능을 위해 코드 데이터가 서버로 전송되며 privacy mode에서는 영구 저장하지 않는다고 명시. 보안 보도는 Cursor, Copilot 등 rule file/prompt injection 취약점을 다룸 | official/security, independent reporting | 중간 | https://www.cursor.com/security ; https://thehackernews.com/2025/09/cursor-ai-code-editor-flaw-enables.html |

## 출처 품질 매트릭스

| 출처 유형 | 개수 | 핵심 기여 | 약점 |
| --- | ---: | --- | --- |
| official / primary | 7 | Anthropic, OpenAI, GitHub, Devin, Replit, Cursor의 제품 기능·내부 도그푸딩·고객 사례 확인 | 성과 수치가 이해관계자 발표이며 실패율/장기 품질 검증이 제한됨 |
| academic / standard / patent | 3 | agentic coding tools 비교, refactoring 연구, prompt injection/MCP tool poisoning 연구로 일반화 가능한 한계 제공 | 업무생산성/비개발 산출물 직접 사례는 아님 |
| direct case / experiment | 8 | Anthropic legal/growth/design/data infra, Nubank, Replit Flash News/UKG, Answer.AI Devin 테스트 | 공개 사례가 성공 편향. 일부는 내부 사례라 독립 검증 어려움 |
| vendor / stakeholder | 8 | 도구별 enterprise positioning, integration, admin/security 기능 파악 | vendor-only 구간은 과장 가능성 큼 |
| independent reporting / analysis | 5 | Axios, Tom's Hardware, Fortune/ITPro 계열, Answer.AI, OECD incident가 vendor narrative를 보정 | 언론은 원출처가 임원 발언/X post인 경우가 있음 |
| community | 6 | Reddit/HN식 실사용 워크플로우와 불만, 비용/데이터/권한 문제 확인 | 익명·검증 불가, 최고 확신도 부여 불가 |
| weak / unverified | 4 | 마케팅 agency/Medium류 사례에서 새로운 패턴 탐색 | 광고성, 과장 가능성, 수치 검증 불가 |

## 반례/실패 사례 검색 로그

| 쿼리 | 목적 | 결과 | 결론 영향 |
| --- | --- | --- | --- |
| `Claude Code enterprise failure` | Claude Code의 공개 기업 실패 사례 확인 | 직접적인 공개 enterprise failure 사례는 미발견. 대신 Anthropic 법무 글이 hallucination과 citation 검증 필요를 명시하고, 커뮤니티에서 data residency/상업 약관/사용량 제한 불만 확인 | Claude Code는 실패 부재가 아니라 공개 실패 사례 부족. 불확실성에 반영 |
| `Codex agent business automation failure` | Codex가 비개발 업무 자동화에서 실패한 사례 확인 | Codex 특정 business automation failure는 직접 증거 미발견. OpenAI는 Codex가 아직 early/research preview였고 image input, course-correction, remote latency 한계를 명시 | Codex의 비개발 자동화 주장은 공식 제품 방향에 가깝고 직접 실패/성공 사례 모두 부족 |
| `AI coding agents production incident` | 운영 사고 검색 | Replit production DB 삭제, AWS AI coding bot 관련 보도, Amazon Q supply-chain성 보도 확인 | 운영/권한 경계가 핵심 리스크라는 결론 강화 |
| `Devin limitations` | Devin 성공 사례 반증 | Answer.AI의 20 task 테스트: 14 실패, 3 성공, 3 불명확. AIAAIC가 이를 incident/automation failure로 정리 | Devin은 대규모 반복 마이그레이션에는 강할 수 있으나 general autonomous engineer 주장은 약화 |
| `Cursor enterprise security concerns` | Cursor 기업 도입 리스크 확인 | Cursor 공식 security/privacy 문서와 Cursor/GitHub Copilot rule file backdoor, AI IDE silent code execution 보도 확인 | enterprise adoption에는 code exfiltration, indirect prompt injection, RCE, model/provider routing 검토 필요 |
| `coding agent case study failed` | case study 실패 사례 일반 검색 | Replit incident, Answer.AI Devin, 커뮤니티 비용/데이터 손실 불만, Copilot agent mode rollout/quality 불만 확인 | 성공 사례의 적용 조건을 명확히 제한해야 함 |
| `Replit Agent limitations failure user experience community` | Replit 커뮤니티 실패 확인 | DB 삭제, app/data deletion, support/refund 불만, prod/dev DB 분리 조언 확인 | Replit은 rapid prototyping엔 강하지만 prod 권한 분리 없이 운영 자동화 금물 |
| `GitHub Copilot agent mode limitations community` | Copilot agent mode 실사용 비판 확인 | rollout 미노출, Ask mode가 Agent로 바뀌는 문제, premium request 비용 불만, 품질이 삽입 가능 수준이 아니라는 댓글 확인 | Copilot은 enterprise governance 강점이 있으나 UX/비용/품질 변동성 존재 |

## 상충점과 불확실성

- **성과 수치 상충**: Anthropic/Replit/Devin 수치는 매우 크지만 대부분 vendor-only다. Answer.AI의 Devin 테스트처럼 독립 실험은 훨씬 낮은 성공률을 보인다. 가능한 해석은 "잘 정의된 반복 작업, 충분한 예시, 권한/테스트/리뷰가 있는 환경에서는 큰 성과"와 "모호한 end-to-end 지식노동에서는 실패율이 높음"이 동시에 참이라는 것이다.
- **비개발 산출물의 정의 불확실성**: 마케팅 카피, 법무 검토, FP&A 보고서, 프로토타입은 비개발 업무지만, 성공한 사례는 거의 모두 코드를 통해 API, 문서 저장소, 브라우저, 디자인 툴, 배포 파이프라인을 조작한다. 즉 "비개발자가 그냥 자연어로 업무를 끝낸다"보다 "업무가 소프트웨어화된다"가 더 정확하다.
- **직접 고객 사례 부족**: Cursor, OpenAI Codex, GitHub Copilot의 공개 자료는 주로 개발 생산성 중심이다. 비개발 업무 자동화/운영 산출물 사례는 Anthropic/Replit에 비해 상대적으로 약하고, 고객명 인용도 정량 검증이 부족하다.
- **보안/컴플라이언스 불확실성**: Cursor 공식 문서처럼 privacy mode, zero retention, 서버 경유 prompt-building, enterprise admin 통제가 있더라도 MCP/tool 권한, repo rule injection, secret exposure는 별도 threat model이 필요하다.
- **시점 리스크**: 2025-2026년 제품 변화가 빠르다. 특정 한계, pricing, admin control, model 성능은 몇 주 단위로 바뀔 수 있어 도입 판단에는 최신 계약서/보안백서/PoC 재검증이 필요하다.

## 의사결정 영향

- 기업이 먼저 시도할 업무는 "API-enabled repetitive tasks"여야 한다. 광고 변형, 보고서 갱신, changelog/release note, 문서/스크린샷 생성, PR triage, CI failure fix, nightly QA, design token audit처럼 입력/출력/검증 기준이 명확한 업무가 우선순위다.
- 비개발 팀 도입은 "에이전트에게 업무 권한을 주는 것"이므로 개발팀의 repo setup, credentials boundary, sandbox, audit log, rollback, production write 권한 차단이 선행되어야 한다.
- vendor-only 수치만으로 ROI를 확정하지 말고, 내부 PoC는 20-50개 실제 업무 backlog로 성공률, human review time, rollback 빈도, 보안 위반, 비용/credit burn, 결과 재사용률을 측정해야 한다.
- 실패 사례는 완전 금지보다 "작업 등급화"를 요구한다. 저위험 산출물은 자동 생성 후 리뷰, 중위험 업무는 PR/approval gate, 고위험 production/data 업무는 read-only 또는 plan-only로 제한하는 방식이 현실적이다.
- 코딩 에이전트가 유용한 조직은 문서/업무 규칙을 `.md`, Skills, runbook, API schema, tests, evals로 관리하는 조직이다. 암묵지와 수동 SaaS UI 클릭에 갇힌 업무는 자동화 전 정리 비용이 크다.

## 인접 질문

1. 각 직무별로 "에이전트가 실행해도 되는 권한"을 read-only, draft-only, PR-only, production-write로 나누면 어떤 governance 모델이 가장 비용 대비 안전한가?
2. 업무 자동화 성공률을 높이는 내부 자산은 무엇인가: 스킬/프롬프트, API schema, 테스트/eval, 데이터 catalog, runbook, 또는 팀별 review rubric 중 무엇이 병목인가?

## 출처 목록

| # | 출처 | 날짜/버전 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| 1 | Anthropic, How Anthropic teams use Claude Code PDF | 2025 | 높음 | https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf |
| 2 | Claude, How Anthropic's legal team cut review times from days to hours with Claude | 2025-12-08 | 높음 | https://claude.com/blog/how-anthropic-uses-claude-legal |
| 3 | OpenAI, Codex product page | 2026-04 확인 | 중간 | https://openai.com/codex |
| 4 | OpenAI, Introducing Codex | 2025-05-16 | 높음 | https://openai.com/index/introducing-codex/ |
| 5 | OpenAI, How OpenAI uses Codex | 2025/2026 확인 | 중간 | https://openai.com/business/guides-and-resources/how-openai-uses-codex/ |
| 6 | GitHub Newsroom, Copilot Introduces Agent Mode | 2025-02-06 | 높음 | https://github.com/newsroom/press-releases/agent-mode |
| 7 | GitHub Blog, GitHub Copilot: The agent awakens | 2025-02-06 | 높음 | https://github.blog/news-insights/product-news/github-copilot-the-agent-awakens/ |
| 8 | Devin/Cognition, Nubank case on Devin homepage | 2026-04 확인 | 중간 | https://devin.ai/ |
| 9 | Replit, Building Mobile Apps on Replit | 2026-02-20 | 중간 | https://blog.replit.com/building-mobile-apps-on-replit |
| 10 | Replit, The Future is Actually Very Human | 2026-03 | 중간 | https://blog.replit.com/replit-raises-400-million-dollars |
| 11 | Cursor, Security | 2025-06-18 | 높음 | https://www.cursor.com/security |
| 12 | Cursor, Privacy Policy | 2025/2026 확인 | 높음 | https://cursor.com/en-US/privacy |
| 13 | Answer.AI, Thoughts On A Month With Devin | 2025-01-08 | 높음 | https://www.answer.ai/posts/2025-01-08-devin.html |
| 14 | AIAAIC, Study: Devin AI software engineer fails at most tasks | 2025-01 | 중간 | https://www.aiaaic.org/aiaaic-repository/ai-algorithmic-and-automation-incidents/study-devin-ai-software-engineer-fails-at-most-tasks |
| 15 | Tom's Hardware, Replit AI coding platform goes rogue | 2025-07-21 | 중간 | https://www.tomshardware.com/tech-industry/artificial-intelligence/ai-coding-platform-goes-rogue-during-code-freeze-and-deletes-entire-company-database-replit-ceo-apologizes-after-ai-engine-says-it-made-a-catastrophic-error-in-judgment-and-destroyed-all-production-data |
| 16 | OECD AI Incident Monitor, Replit AI Coding Tool Deletes Live Production Database | 2025-07-19 | 중간 | https://oecd.ai/en/incidents/2025-07-19-1eb1 |
| 17 | The Hacker News, Cursor AI Code Editor Flaw Enables Silent Code Execution | 2025-09-12 | 중간 | https://thehackernews.com/2025/09/cursor-ai-code-editor-flaw-enables.html |
| 18 | Axios, Anthropic bolsters enterprise offerings with Cowork plugins | 2026-01-30 | 중간 | https://www.axios.com/2026/01/30/ai-anthropic-enterprise-claude |
| 19 | Tom's Hardware, NVIDIA internal Cursor deployment | 2026-02-09 | 중간 | https://www.tomshardware.com/tech-industry/artificial-intelligence/nvidia-now-produces-three-times-as-much-code-as-before-ai-specialized-version-of-cursor-is-being-used-by-over-30-000-nvidia-engineers-internally |
| 20 | Reddit r/ClaudeAI, Automating the Software to Marketing Pipeline with Claude Code | 2026-03 | 낮음 | https://www.reddit.com/r/ClaudeAI/comments/1rixfe2/automating_the_software_to_marketing_pipeline/ |
| 21 | Reddit r/FPandA, Claude Code Use Cases? | 2026-03 | 낮음 | https://www.reddit.com/r/FPandA/comments/1rjpdfv/claude_code_use_cases/ |
| 22 | Reddit r/replit, Replit Agent deleted a production DB discussion | 2025-07 | 낮음 | https://www.reddit.com/r/replit/comments/1m5biur |
| 23 | Reddit r/cursor, Cursor pricing/security/community complaints | 2025-2026 | 낮음 | https://www.reddit.com/r/cursor/comments/1lrlb6m |
| 24 | arXiv, Comparing AI Coding Agents: A Task-Stratified Analysis of Pull Request Acceptance | 2026-02 | 중간 | https://arxiv.org/abs/2602.08915 |
| 25 | arXiv, Agentic Refactoring: An Empirical Study of AI Coding Agents | 2025-11 | 중간 | https://arxiv.org/abs/2511.04824 |
| 26 | arXiv, Your AI, My Shell: Prompt Injection Attacks on Agentic AI Coding Editors | 2025-09 | 중간 | https://arxiv.org/abs/2509.22040 |
| 27 | arXiv, Are AI-assisted Development Tools Immune to Prompt Injection? | 2026-03 | 중간 | https://arxiv.org/abs/2603.21642 |

## 검색 포화 판단

깊이 게이트는 충족했다. official/primary는 Anthropic, Claude, OpenAI, GitHub, Devin, Replit, Cursor에서 3개 이상 확보했고, 직접 사례는 Anthropic 내부 4개 팀, Devin/Nubank, Replit/UKG와 Flash News, Answer.AI hands-on까지 4개 이상 확인했다. 독립 보도/분석은 Answer.AI, Axios, Tom's Hardware, OECD incident, AIAAIC로 2개 이상 확보했다. 커뮤니티 실사용/비판은 Reddit의 Claude Code marketing pipeline, FP&A use case, Replit incident, Cursor pricing/security 불만으로 2개 이상 확보했다. 실패/한계 검색은 Devin limitations, Replit production incident, Cursor enterprise security concerns, Codex/Claude failure negative target을 수행했다.

검색 포화의 근거는 새 검색이 같은 사례군을 반복했다는 점이다. 긍정 사례는 Anthropic/Replit/Devin 공식자료와 일부 언론 재인용으로 수렴했고, 실패 사례는 Answer.AI Devin 테스트와 Replit DB 삭제, AI IDE prompt-injection/security 취약점으로 수렴했다. 아직 부족한 직접 증거는 OpenAI Codex와 GitHub Copilot agent mode가 비개발 산출물 제작에 쓰인 공개 기업 사례, Claude Code의 명시적 enterprise failure 사례, Codex agent의 business automation failure 사례다. 다음 라운드에서는 고객 보안백서, SOC2/DPA, 엔터프라이즈 PoC 발표 자료, 컨퍼런스 세션 녹취를 추가로 확인해야 한다.
