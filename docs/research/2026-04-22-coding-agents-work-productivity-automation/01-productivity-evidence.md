# 측정된 생산성/업무 성과 근거 - 코딩 에이전트 기반 업무 개선

**Researcher**: R1  
**Mode**: mixed  
**Date**: 2026-04-22  
**Scope**: GitHub Copilot, AI coding agents, Claude/Codex 계열 워크플로우와 연결 가능한 실험/현장 연구, 컨설팅/학술 보고서, 벤치마크 신뢰성, 소프트웨어 개발 외 지식근로 생산성 근거. 최종 synthesis는 포함하지 않음.

## 핵심 요약

측정 근거는 “AI가 항상 개발자를 빠르게 한다”가 아니라 “업무가 잘 구조화되고 성공 기준이 명확할수록 초안 생성, 반복 작업, 문서화, 테스트 보조, 지식 검색에서 생산성 상승이 크다”는 쪽으로 수렴한다. GitHub Copilot 단일 과제 실험은 2022-2023년 JavaScript HTTP 서버 구현에서 55.8% 빠른 완료를 보였고, Microsoft/Accenture/Fortune 100 현장 RCT는 4,867명 통합 분석에서 완료 작업 수 26.08% 증가를 보고했다. 그러나 저순응, 기업별 잡음, 산출량 중심 지표라는 한계가 크다.

소프트웨어 밖 지식근로 실험은 코딩 에이전트식 워크플로우를 “문서/분석/초안/검토의 재설계”로 확장할 때의 근거를 제공한다. 고객지원 현장 연구는 5,172명 규모에서 해결 건수/시간이 약 13.8-15% 증가했고, BCG 컨설턴트 실험은 GPT-4가 적합한 과제에서 속도 25%+, 인간 평가 품질 40%+, 완료 과제 12%+를 보였다. P&G 신제품 혁신 실험은 개인+AI가 사람 팀 수준 성과를 냈다는 점에서 작은 팀의 레버리지와 handoff 감소 가능성을 지지한다.

반대 근거도 강하다. METR의 2025년 RCT는 숙련 OSS 개발자 16명이 자신이 잘 아는 저장소의 실제 이슈 246개를 처리할 때 AI 허용 조건이 오히려 19% 느렸다고 보고했다. DORA 2024는 AI 채택 25% 증가가 문서/코드 품질 및 리뷰 속도 개선과 함께 delivery throughput 1.5% 감소, delivery stability 7.2% 감소와 연관된다고 보고했다. 즉 생산성 편익은 검토/테스트/릴리스 운영 병목을 줄이는 workflow redesign 없이는 상쇄될 수 있다.

## 주요 발견

1. **개별 코딩 과제의 속도 개선은 반복적으로 관측되지만, 일반화 범위가 좁다.**  
   Peng et al.의 Copilot 실험은 recruited developer가 JavaScript HTTP server를 빨리 구현하는 과제에서 AI 사용군이 55.8% 빠르게 끝냈다. GitHub는 동일 결과를 평균 1시간 11분 대 2시간 41분, p=.0017, 95% CI 21-89%로 공개했다. 조건은 짧고 고립된 greenfield 과제이며, 대규모 레거시 코드베이스나 다단계 요구사항 처리에는 직접 일반화하기 어렵다.

2. **현장 RCT는 효과가 존재하되 채택률과 측정 방식에 민감하다.**  
   Microsoft Research/MIT 계열 2025년 논문은 Microsoft, Accenture, Fortune 100 기업 RCT를 통합해 4,867명 기준 완료 작업 수 26.08%(SE 10.3%) 증가를 보고했다. 그러나 부록의 ITT 분석은 Microsoft/Accenture 초기 구간에서 Accenture builds를 제외하면 “처치 배정” 자체의 통계적으로 유의한 효과가 없고, Microsoft 44.2%, Accenture 61.7%의 낮은 초기 채택률이 해석을 어렵게 한다.

3. **업무 산출물 생성으로 확장하면 효과는 문서화, 초안, 고객지원, 컨설팅형 분석에서 더 명확하다.**  
   McKinsey의 40명+ 실험은 코드 생성, 리팩터링, 문서화에서 AI 사용군/통제군 교차 설계를 썼고, 문서화와 반복 코딩에서 큰 절감 가능성을 보고했다. NBER/QJE 고객지원 연구는 AI가 고성과자의 암묵지를 초보자에게 전파하는 형태로 낮은 숙련자에게 더 큰 효과를 냈다. 이는 코딩 에이전트를 “코드 작성기”보다 “업무 산출물 생성 및 절차화 도구”로 볼 때 더 설득력이 커진다.

4. **AI는 workflow redesign의 대체재가 아니라 증폭기다.**  
   DORA 2024는 AI 채택 증가가 문서 품질 7.5%, 코드 품질 3.4%, 코드 리뷰 속도 3.1% 증가와 연관됐지만 delivery stability는 7.2% 감소했다고 보고했다. DORA 2025의 공개 요약은 다수 개발자가 생산성 향상을 체감하고 코드 품질 긍정 응답이 59%라고 하지만, 안정성 문제는 계속 남아 있다고 설명한다. 즉 코딩 단계 속도가 빨라져도 리뷰, 테스트, 변경 관리, 운영 검증이 병목이면 전체 성과는 악화될 수 있다.

5. **에이전트/벤치마크 점수는 업무 생산성의 충분조건이 아니다.**  
   SWE-bench Verified는 기존 SWE-bench의 모호한 이슈, 과도하게 특정한 테스트, 환경 재현 실패를 줄이기 위해 93명의 Python 개발자 검수를 거친 500개 샘플을 냈다. OpenAI도 정적 공개 GitHub 기반 벤치마크는 오염 가능성과 좁은 분포라는 한계를 명시했다. UTBoost는 SWE-bench의 불충분한 테스트가 오류 패치를 통과 처리할 수 있으며, leaderboard entry의 40.9%(Lite), 24.4%(Verified)에 영향을 준다고 보고했다. 따라서 Codex/Claude Code 벤치마크 점수는 “가능성”이지 “현장 ROI”가 아니다.

## 근거 표

| 주장 | 근거 | 출처 유형 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| Copilot은 짧고 명확한 greenfield 코딩 과제에서 완료 시간을 크게 줄였다. | 2022-2023년 실험: JavaScript HTTP server 구현, treatment가 55.8% 빠름. GitHub 공개 수치: 평균 1:11 vs 2:41, p=.0017, 95% CI 21-89%. 한계: 단일 과제, 단기, 실제 레거시 워크플로우 아님. | academic + official | 높음 | https://arxiv.org/abs/2302.06590 ; https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/ |
| 기업 현장 RCT에서는 Copilot 접근/사용이 완료 작업 수를 늘릴 수 있으나 채택률과 통계 파워가 중요하다. | Microsoft/Accenture/Fortune 100 RCT, 4,867명 통합, completed tasks +26.08%(SE 10.3%). 한계: 회사별 noisy, 초기 ITT 다수 비유의, 산출량 지표 중심. | academic/report + primary | 중상 | https://economics.mit.edu/sites/default/files/inline-files/draft_copilot_experiments.pdf |
| OSS 협업에서는 AI가 코드 기여를 늘리는 동시에 조정 비용을 늘릴 수 있다. | GitHub proprietary Copilot usage + OSS 데이터 분석: project-level code contributions +5.9%, individual +2.1%, participation +3.4%, coordination time +8%. 한계: arXiv preprint, 인과 추정 설계 세부 검토 필요. | academic/preprint | 중 | https://arxiv.org/abs/2410.02091 |
| 고객지원 같은 반복 지식업무에서는 AI가 저숙련자에게 특히 큰 생산성 효과를 낸다. | 5,172명 customer support field data, staggered rollout; QJE판 표의 preferred spec은 RPH +0.301, 평균 대비 약 13.8%, arXiv/NBER 요약은 14-15% 내외. 한계: 단일 Fortune 500 소프트웨어 고객지원, 제품/프로세스 안정성이 높은 환경. | peer-reviewed academic | 높음 | https://academic.oup.com/qje/article/140/2/889/7990658 ; https://arxiv.org/abs/2304.11771 |
| 전문 지식근로에서도 “AI frontier 안” 과제는 속도/품질 개선이 크다. | 2023년 GPT-4, 758 BCG consultants, realistic business tasks; Organization Science 2026: 속도 25%+, 성과 30%+, 완료 12%+; Harvard D3/working paper 요약은 human-rated performance 40%+ 개선. 한계: 컨설팅 과제, 평가 주관성, BCG/연구진 협업. | peer-reviewed academic + institutional | 높음 | https://pubsonline.informs.org/doi/10.1287/orsc.2025.21838 ; https://d3.harvard.edu/navigating-the-jagged-technological-frontier/ |
| 같은 BCG 실험에서 “AI frontier 밖” 과제는 품질을 악화시켰다. | 복잡한 managerial task에서 AI 사용군은 통제군보다 정답 가능성이 19% 낮음; control 84.5%, AI 조건 60%/70.6%. 한계: 특정 과제로 설계된 outside-frontier 사례. | peer-reviewed academic | 높음 | https://pubsonline.informs.org/doi/10.1287/orsc.2025.21838 |
| AI는 일부 팀 협업 기능을 대체/재구성해 작은 팀 레버리지를 높일 수 있다. | NBER 2025 P&G RCT, 776명, 실제 product innovation challenge; individuals with AI matched teams without AI, functional silos 완화. 한계: working paper, P&G 지원/이해관계 disclosure, 수치 세부는 PDF 추가 검토 필요. | academic/report direct experiment | 중상 | https://www.nber.org/papers/w33641 |
| 숙련 개발자의 실제 저장소 업무에서는 AI가 느리게 만들 수 있다. | METR 2025 RCT: 16명 experienced OSS developers, 246 tasks, 평균 2시간, 주로 Cursor Pro + Claude 3.5/3.7 Sonnet, Feb-Jun 2025 frontier; AI 허용 시 완료 시간이 19% 증가. 한계: 표본 16명, 특정 OSS maintainer, Cursor 미숙련 일부. | independent report / direct experiment | 높음 | https://metr.org/Early_2025_AI_Experienced_OS_Devs_Study-paper.pdf |
| AI 채택은 개발자 체감 생산성과 일부 품질 지표를 높이지만 릴리스 안정성을 악화시킬 수 있다. | DORA 2024: AI adoption +25%와 documentation quality +7.5%, code quality +3.4%, code review speed +3.1%, throughput -1.5%, stability -7.2% 연관. 한계: survey/correlation, 자기보고 지표 포함. | official/report | 중상 | https://cloud.google.com/blog/products/devops-sre/announcing-the-2024-dora-report |
| 개발자 신뢰와 검증 부담은 생산성 편익의 주요 상쇄 요인이다. | Stack Overflow 2025: AI output 정확성을 distrust 46%, trust 33%, high trust 3.1%; deployment/monitoring 75.8%, project planning 69.2%는 AI 사용 계획 없음. 한계: 자기선택 survey, 응답자 구성 편향. | primary survey | 중 | https://survey.stackoverflow.co/2025/ai |
| 벤치마크는 코딩 에이전트 업무성과를 과대/과소평가할 수 있다. | OpenAI SWE-bench Verified: 기존 SWE-bench의 모호한 issue, 과특정 테스트, 환경 실패 문제 지적; 정적 공개 GitHub 데이터 오염 가능성 명시. UTBoost: 불충분 테스트로 345 erroneous patches가 pass 처리, Lite/Verified leaderboard entry 40.9%/24.4% 영향. | official + academic | 높음 | https://openai.com/index/introducing-swe-bench-verified/ ; https://arxiv.org/abs/2506.09289 |
| 보안/품질 리스크는 “빠른 생성” 이득을 잠식한다. | SecureVibeBench 2026 ACL 예정: 105개 C/C++ secure coding tasks, multi-file large repo; 최고 에이전트도 correct-and-secure 23.8%. 한계: 벤치마크, 실제 조직 프로세스와 다름. | academic/preprint | 중상 | https://arxiv.org/abs/2509.22097 |

## 출처 품질 매트릭스

| 출처 유형 | 개수 | 핵심 기여 | 약점 |
| --- | ---: | --- | --- |
| official / primary | 5 | GitHub Copilot 실험 공개값, Microsoft Research 논문 페이지, DORA, OpenAI SWE-bench Verified, Stack Overflow survey | GitHub/OpenAI/Microsoft는 이해관계자. Stack Overflow는 자기선택 survey |
| academic / standard / patent | 9 | arXiv/working paper/QJE/Organization Science/NBER/ACL 근거로 실험 설계와 한계 확인 | 일부는 preprint 또는 working paper, 최신 연구는 peer review 전 |
| direct case / experiment | 7 | GitHub Copilot controlled experiment, Microsoft/Accenture/F100 RCT, METR RCT, NBER customer support, BCG, P&G, McKinsey lab | 실제 장기 조직 ROI와 완전히 같지 않음 |
| vendor / stakeholder | 4 | GitHub, McKinsey, BCG, Google/DORA의 산업 측정값 | 홍보/선택 편향 가능성, 원자료 제한 |
| community | 0 | 본 R1 범위에서는 커뮤니티 근거를 핵심 증거로 사용하지 않음 | 현장 감각은 덜 반영 |
| weak / unverified | 0 | 표의 핵심 주장에는 사용하지 않음 | 최신 보도 일부는 검색 로그에만 반영 |

## 반례/실패 사례 검색 로그

| 쿼리 | 목적 | 결과 | 결론 영향 |
| --- | --- | --- | --- |
| `METR AI tools slow down experienced developers 19 percent randomized trial 2025` | 숙련 개발자 생산성 저하 직접증거 확인 | METR RCT 원문 PDF와 Ars/TechCrunch 보도 발견. 원문 기준 16명, 246 실제 OSS tasks, AI 허용 시 19% 느림. | “숙련자+익숙한 코드베이스+복잡한 실제 이슈”에서는 총생산성이 떨어질 수 있음을 강하게 반영 |
| `AI coding assistant productivity failure generative AI productivity slowdown` | AI 생산성 실패/저하 사례 탐색 | METR, DORA 2024 delivery stability/throughput 악화, Stack Overflow trust 하락 발견 | 단순 시간 절감 주장은 workflow 병목과 검증 비용을 포함해야 함 |
| `Copilot productivity limitation real world projects large codebase proprietary context` | Copilot 한계 업무 유형 확인 | 2024 arXiv real-world projects는 문서화/반복 작업은 강하지만 complex tasks, large functions, multiple files, proprietary contexts, C/C++에서 어려움 보고 | “업무 산출물 생성” 중에서도 긴 컨텍스트/다파일/도메인 지식 과제는 제한적 |
| `AI agent benchmark reliability SWE-bench limitations contamination 2025` | 벤치마크 점수와 실제 업무성과 간 괴리 확인 | OpenAI SWE-bench Verified 한계, UTBoost 불충분 테스트, SWE-EVO 장기 과제 격차 발견 | Codex/Claude Code 벤치마크를 ROI 근거로 직접 쓰지 않도록 경고 |
| `generative AI productivity slowdown knowledge worker outside frontier BCG` | 소프트웨어 외 지식근로 반례 확인 | BCG/Organization Science: outside frontier managerial task에서 AI 사용군 정답률 19%p 낮음 | 업무 재설계에는 “AI가 잘하는 과제 경계” 판단 절차가 필요 |
| `AI generated code verification debt developers review more effort` | 검토 부담과 오류 수정 비용 근거 확인 | Sonar 보도: AI 생성 코드 검토가 동료 코드보다 더 힘들다는 응답 38%, AI code looks correct but unreliable 61% 보도. 원문 vendor survey라 핵심 표에는 보조로만 반영 | 검증 부채가 편익을 상쇄할 수 있다는 불확실성 강화 |
| `Secure code generation code agents realistic vulnerability benchmark correct secure 2026` | 보안 리스크가 자동화 편익을 상쇄하는 조건 탐색 | SecureVibeBench: 최고 에이전트도 correct-and-secure 23.8% | 보안 민감 코드/업무 자동화는 별도 보안 오라클과 human gate 필요 |

## 상충점과 불확실성

- **짧은 과제와 실제 업무의 차이**: Copilot 55.8% 개선은 강한 실험 근거지만, 짧고 독립적인 HTTP server 구현 과제다. 반대로 METR은 실제 OSS 이슈를 썼지만 표본 16명으로 작고 숙련 maintainer 중심이다. 둘은 모순이라기보다 과제 구조와 코드베이스 친숙도 차이를 보여준다.
- **생산성 지표의 정의 차이**: pull request, commits, builds, resolved chats/hour, task completion time, subjective productivity, quality rating은 서로 대체 불가능하다. 코딩 에이전트의 업무 자동화 가치는 “코드량”보다 handoff 감소, 재현성, 승인/리뷰 주기 단축, 문서 품질에 나타날 수 있다.
- **독립 검증과 vendor-only 구간**: GitHub/Accenture, McKinsey, BCG 일부 자료는 이해관계자가 포함된다. QJE/NBER, Organization Science, METR, ACL/arXiv는 더 독립적이지만 최신 preprint는 아직 검증 중이다.
- **학습효과와 모델 세대 효과**: METR은 early-2025 frontier(Cursor Pro + Claude 3.5/3.7 Sonnet) 조건이다. Claude Code, Codex, GPT-5.x 계열의 2026년 agentic workflow에는 직접 동일하게 적용할 수 없다. 다만 “검토/대기/프롬프팅/컨텍스트 복구 비용”이라는 메커니즘은 여전히 관련성이 높다.
- **품질/보안 리스크의 비용화 부족**: 대부분 실험은 장기 유지보수, 보안 취약점, incident cost, onboarding debt를 충분히 추적하지 않는다. DORA와 SecureVibeBench는 이 공백을 보완하지만 조직별 운영 성숙도에 따라 영향이 크게 달라질 수 있다.

## 의사결정 영향

- 코딩 에이전트를 도입할 때 ROI 가설은 “개발자당 시간 절감”보다 “반복 산출물 생성, 문서/테스트/리뷰 준비, 데이터/스크립트 파이프라인 초안, 표준 운영 절차 자동화”로 설계하는 편이 근거와 더 잘 맞는다.
- 우선 적용 업무는 성공 기준이 명확하고 검증 자동화가 가능한 영역이어야 한다. 예: 문서 초안, 테스트 생성 초안, 코드 설명, migration checklist, 내부 도구 스크립트, 반복적인 데이터 변환, PR 설명/리뷰 준비.
- 고위험 영역은 별도 게이트가 필요하다. 예: 보안 민감 코드, 다파일 아키텍처 변경, 배포/모니터링 자동화, project planning, 규제 문서. Stack Overflow 2025에서 개발자들이 가장 꺼리는 영역도 deployment/monitoring과 project planning이었다.
- 조직 측정은 최소 세 층으로 분리해야 한다. 1) 개인 task cycle time, 2) 팀 handoff/review/rework rate, 3) delivery stability/change failure/incident. DORA 2024가 보여주듯 1층이 좋아져도 3층은 악화될 수 있다.
- 벤치마크는 모델/도구 후보 선별용으로만 쓰고, 구매/확대 결정은 내부 과제 샘플 RCT 또는 stepped rollout으로 검증해야 한다. 공개 SWE-bench류 점수는 static dataset, contamination, insufficient tests, scaffold effect 때문에 현장 생산성의 대리변수로 약하다.

## 인접 질문

- 같은 코딩 에이전트가 “개발자 작업”보다 “운영/분석/문서/QA/데이터 파이프라인”에서 더 큰 ROI를 내는 조직 조건은 무엇인가?
- AI가 만든 산출물의 검토 비용, 보안 비용, incident 비용을 포함한 net productivity를 어떤 표준 지표로 측정할 수 있는가?

더 나은 문제 정의 제안: “코딩 에이전트가 코드를 얼마나 빨리 쓰는가”보다 “검증 가능한 업무 산출물의 생성-검토-배포 흐름에서 어느 병목을 줄이고 어느 병목을 새로 만드는가”로 질문을 재정의하는 것이 의사결정에 더 직접적이다.

## 출처 목록

| # | 출처 | 날짜/버전 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| 1 | Peng et al., The Impact of AI on Developer Productivity: Evidence from GitHub Copilot | arXiv v1, 2023-02-13 | 높음 | https://arxiv.org/abs/2302.06590 |
| 2 | GitHub Blog, Research: quantifying GitHub Copilot’s impact on developer productivity and happiness | 2022-09-07 | 높음 | https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/ |
| 3 | Cui et al., The Effects of Generative AI on High-Skilled Work: Evidence from Three Field Experiments with Software Developers | draft, 2025-02 / Microsoft Research page 2025-06 | 중상 | https://economics.mit.edu/sites/default/files/inline-files/draft_copilot_experiments.pdf |
| 4 | MIT GenAI preview, Productivity Effects of Generative AI with GitHub Copilot | 2024-03-27 | 중 | https://mit-genai.pubpub.org/pub/v5iixksv |
| 5 | Song, Agarwal, Wen, The Impact of Generative AI on Collaborative Open-Source Software Development | arXiv v2, 2025-07-08 | 중 | https://arxiv.org/abs/2410.02091 |
| 6 | Brynjolfsson, Li, Raymond, Generative AI at Work | QJE 140(2), 2025; NBER/arXiv 2023 | 높음 | https://academic.oup.com/qje/article/140/2/889/7990658 |
| 7 | Dell'Acqua et al., Navigating the Jagged Technological Frontier | Organization Science 37(2), published online 2026-03-11 | 높음 | https://pubsonline.informs.org/doi/10.1287/orsc.2025.21838 |
| 8 | Harvard D3, Navigating the Jagged Technological Frontier summary | 2023-09-21 | 중상 | https://d3.harvard.edu/navigating-the-jagged-technological-frontier/ |
| 9 | Dell'Acqua et al., The Cybernetic Teammate | NBER Working Paper 33641, 2025-04 | 중상 | https://www.nber.org/papers/w33641 |
| 10 | METR, Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity | paper, 2025 | 높음 | https://metr.org/Early_2025_AI_Experienced_OS_Devs_Study-paper.pdf |
| 11 | Google Cloud/DORA, Announcing the 2024 DORA report | 2024 | 중상 | https://cloud.google.com/blog/products/devops-sre/announcing-the-2024-dora-report |
| 12 | DORA 2024 Accelerate State of DevOps Report | 2024 report | 중상 | https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf |
| 13 | Google, How are developers using AI? Inside Google's 2025 DORA report | 2025 | 중 | https://blog.google/innovation-and-ai/technology/developers-tools/dora-report-2025/ |
| 14 | Stack Overflow Developer Survey 2025, AI section | 2025 | 중 | https://survey.stackoverflow.co/2025/ai |
| 15 | McKinsey, Unleashing developer productivity with generative AI | 2023-06-27 | 중 | https://www.mckinsey.com/capabilities/tech-and-ai/our-insights/unleashing-developer-productivity-with-generative-ai |
| 16 | Pandey et al., Transforming Software Development: Evaluating the Efficiency and Challenges of GitHub Copilot in Real-World Projects | arXiv, 2024-06-25 | 중 | https://arxiv.org/abs/2406.17910 |
| 17 | OpenAI, Introducing SWE-bench Verified | 2024 | 높음 | https://openai.com/index/introducing-swe-bench-verified/ |
| 18 | Yu et al., UTBoost: Rigorous Evaluation of Coding Agents on SWE-Bench | ACL 2025 / arXiv 2025-06-10 | 높음 | https://arxiv.org/abs/2506.09289 |
| 19 | Thai et al., SWE-EVO: Benchmarking Coding Agents in Long-Horizon Software Evolution Scenarios | arXiv v5, 2025-12-20 | 중 | https://arxiv.org/abs/2512.18470 |
| 20 | Chen et al., SecureVibeBench: Evaluating Secure Coding Capabilities of Code Agents with Realistic Vulnerability Scenarios | arXiv v3, 2026-04-11; ACL 2026 Main 예정 | 중상 | https://arxiv.org/abs/2509.22097 |
| 21 | Noy and Zhang, Experimental evidence on the productivity effects of generative artificial intelligence | Science 381, 2023 | 높음 | https://economics.mit.edu/sites/default/files/inline-files/Noy_Zhang_1.pdf |
| 22 | NBER, Workplace Adoption of Generative AI / Rapid Adoption of Generative AI | 2024 | 중 | https://www.nber.org/digest/202412/workplace-adoption-generative-ai |

## 검색 포화 판단

검색 깊이 게이트는 충족했다. 공식/1차 출처는 GitHub, Microsoft Research, Google/DORA, OpenAI, Stack Overflow로 2개 이상 확인했다. academic/report는 QJE, Organization Science, NBER, arXiv/ACL, MIT draft 등 3개 이상 확인했다. 직접 실험/현장 사례는 Copilot controlled experiment, Microsoft/Accenture/F100 RCT, METR RCT, NBER customer support, BCG, P&G로 2개 이상 확인했다. 반례/한계 검색은 METR slowdown, DORA stability/throughput 악화, BCG outside-frontier, SWE-bench/UTBoost benchmark reliability, SecureVibeBench security failure로 2개 이상 수행했다.

검색 포화 근거: 반복 검색에서 새 독립 증거 유형은 크게 늘지 않고, 동일 축(단기 코딩 속도 개선, 지식업무 초안/지원 개선, 숙련자/복잡 과제 slowdown, 벤치마크/보안 한계)으로 수렴했다. 남은 부족 항목은 2026년 현재 Codex/Claude Code 자체의 장기 기업 내부 RCT와 총소유비용(TCO), incident/rework cost까지 포함한 공개 net productivity 연구다. 다음 라운드에서는 특정 기업의 내부 stepped rollout 설계, 로그 기반 productivity telemetry, 보안/품질 비용 계량 연구를 별도 viewpoint로 조사해야 한다.
