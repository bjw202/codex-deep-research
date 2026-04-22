# Repair Notes - 코딩 에이전트의 업무생산성 향상과 혁신/자동화

## 검증된 결함

### RQ-01: official/vendor 성과 수치의 확신도 분리
- target file: `02-enterprise-cases.md`, `97-journal.md`
- original claim: Anthropic 내부 사례 일부가 `official/primary, direct case, vendor-only | 높음`으로, Journal도 Anthropic 법무팀의 turnaround 감소를 `높음`으로 표기한다.
- cited source: Anthropic Claude Code PDF, Claude legal blog, Devin homepage, Replit funding blog.
- source check result: supported with calibration issue. Anthropic PDF 원문은 성장마케팅 광고 카피가 2시간에서 15분, creative output 10x, 제품디자인 2-3x 실행을 주장한다. Claude legal blog는 마케팅 리뷰 turnaround가 2-3일에서 24시간으로 감소했다고 밝힌다. Devin 홈페이지는 Nubank migration에서 8-12x efficiency와 20x cost saving을 주장하며 계산 기준을 설명한다. Replit 블로그는 UKG의 feedback gathering ability 400% 증가를 주장한다. 그러나 모두 official/vendor/customer story이며 독립 대조군, 장기 품질, 오류율, 재무성과 검증은 원문에서 확인되지 않는다.
- correction: `확신도 높음`은 `출처 존재/수치 원문 확인: 높음`과 `효과 크기/ROI 확신도: 중간 또는 낮음`으로 분리해야 한다. Anthropic 내부 운영 사실과 수치 존재는 높음, 효과 크기의 일반화와 재무성과는 중간 이하로 표기한다. Devin/Replit은 이미 중간이지만 `direct case` 옆에 `vendor/customer story, not independently audited`를 명시한다.
- confidence: 높음

### RQ-02: Codex use cases의 direct case 오분류
- target file: `03-workflow-patterns.md`
- original claim: 출처 품질 매트릭스에서 `direct case / experiment` 5개에 `Codex workflow examples`를 포함하고, 검색 포화 판단에서 `Codex use-case recipes`를 직접 workflow 사례로 계산한다.
- cited source: OpenAI Codex use cases, Codex slide deck use case, Codex QA/inbox/use case 문서.
- source check result: supported. Codex use cases 원문은 slide decks, inbox, QA, tabular data 등 공식 use-case catalog와 recipe를 제공한다. slide deck 페이지도 PptxGenJS, render/validation, overflow/font checks 같은 권장 workflow를 설명한다. 이는 공식 제품 문서/recipe이지 특정 고객 또는 실험의 성과 사례가 아니다.
- correction: `Codex workflow examples`는 `official product recipe/documentation`으로 재분류한다. `direct case / experiment` 카운트에서는 제외하고, R3의 직접 사례는 Block, Graphite, CodeRabbit, GitHub issue-to-PR 제품 시연/블로그, 학술 agentic PR 연구 등으로 제한한다. Codex use cases는 기능·권장 패턴 근거로 유지하되 성과 실증으로 쓰지 않는다.
- confidence: 높음

### RQ-03: 제품 로드맵/모델 성능 발표의 ROI 과잉 해석 위험
- target file: `05-future-impact.md`
- original claim: R5는 Codex, GPT-5.2/5.3-Codex, Claude Code, Microsoft/GitHub governance 자료를 향후 조직 변화와 ROI 프레임의 근거 축에 함께 배치한다.
- cited source: OpenAI Codex GA, Codex for almost everything, GPT-5.2-Codex, GPT-5.3-Codex, Anthropic Claude Code docs/news, Microsoft/GitHub governance 자료.
- source check result: supported with overinterpretation risk. OpenAI 원문은 Slack integration, SDK, admin tools, computer use, memory, automations, long-horizon work, tool use, benchmark/cyber capability 등 capability와 product direction을 확인한다. GPT-5.3-Codex 원문도 professional work on a computer와 benchmark performance를 설명한다. 하지만 해당 원문들은 장기 기업 ROI, 조직 구조 변화, net productivity를 독립 실증하지 않는다.
- correction: R5의 로드맵/모델 성능 항목은 `capability/direction evidence: 높음`으로 두고, `ROI/조직 변화 실증: 낮음 또는 별도 증거 필요`를 명시한다. ROI 문장은 allpay/Dow/Salesforce/Accenture 같은 stakeholder case와 METR/NBER 등 실증 연구로 분리해 써야 하며, 제품 release note를 ROI 근거로 병렬 배치하지 않는다.
- confidence: 높음

### RQ-04: MIT NANDA 95% zero return 약한 근거 처리
- target file: `05-future-impact.md`, `97-journal.md`
- original claim: R5는 Gartner와 MIT NANDA를 같은 근거 행에서 `analyst/report | 중`으로 배치하고, Journal은 MIT NANDA를 `중` 및 약한 증거 구간으로 기록한다.
- cited source: `https://www.artificialintelligence-news.com/wp-content/uploads/2025/08/ai_report_2025.pdf`, 언론 재인용 검색 결과.
- source check result: supported with weak-source caveat. PDF mirror 원문은 $30-40B enterprise GenAI investment에도 95%가 zero return, 5%만 production value를 낸다고 적고 있다. 그러나 인용 URL은 MIT 공식 배포 경로가 아니라 언론 사이트의 PDF mirror이며, 검색 결과도 다수 언론/블로그 재인용과 다른 mirror PDF에 의존한다. 원 배포 경로, 표본, zero return 정의, 방법론 세부는 현재 인용만으로 강하게 검증되지 않는다.
- correction: MIT NANDA 주장은 `weak/report mirror; 반례 신호`로 유지한다. Gartner forecast, METR RCT, NBER/QJE field study와 같은 강도의 실증 근거로 병렬 배치하지 않는다. 문장 강도는 `기업 GenAI ROI 실패 담론의 경고 신호`로 낮추고, `95% zero return`은 직접 실측 일반명제가 아니라 방법론 추가 검증 필요 항목으로 표시한다.
- confidence: 중상

### RQ-05: 생산성 수치 표의 metric unit 명시
- target file: `01-productivity-evidence.md`, `97-journal.md`
- original claim: 생산성 수치 표가 Copilot 55.8%, field RCT +26.08%, customer support 13.8-15%, BCG 25%/40%/12%, METR 19%, DORA 7.5%/3.4%/3.1%/-1.5%/-7.2%를 함께 나열한다.
- cited source: R1의 근거 표와 Journal 핵심 주장 표.
- source check result: supported. 각 수치는 서로 다른 metric unit을 가진다. Copilot은 task completion time, field RCT는 completed tasks, customer support는 resolutions per hour 또는 issue resolution throughput, BCG는 speed/human-rated quality/completion, METR은 completion time, DORA는 survey/correlation 기반 documentation quality/code quality/review speed/throughput/stability다.
- correction: 각 수치 옆에 metric unit을 명시해야 한다. 권장 표기: `55.8% faster task completion time`, `completed tasks +26.08%`, `RPH/resolutions per hour +0.301 또는 약 +13.8-15%`, `speed +25%, human-rated quality/performance +40%, task completion +12%`, `completion time +19%`, `DORA documentation quality/code quality/review speed/throughput/stability association`. Synthesis에서는 이들을 단일 `생산성 %`로 평균내지 않는다.
- confidence: 높음

## 정정 요약

| repair_id | status | correction | confidence |
| --- | --- | --- | --- |
| RQ-01 | supported | official/vendor 수치는 `출처 존재 높음`과 `효과 크기/ROI 확신도 중간 또는 낮음`으로 분리 | 높음 |
| RQ-02 | supported | Codex use cases/workflow examples는 direct case/experiment가 아니라 official product recipe/documentation으로 재분류 | 높음 |
| RQ-03 | supported | 제품 로드맵과 모델 성능 발표는 capability/direction 근거로 제한하고 ROI/조직 변화 실증과 분리 | 높음 |
| RQ-04 | supported | MIT NANDA 95% zero return은 mirror/언론 재인용 기반 약한 반례 신호로 유지 | 중상 |
| RQ-05 | supported | 생산성 수치 표에 metric unit을 붙이고 단일 생산성 지표처럼 혼합하지 않음 | 높음 |

## 남은 미해결 항목

- RQ-04: MIT NANDA 원 배포 경로, 표본 설계, `zero return` 및 `production value` 정의는 현재 mirror PDF와 언론 재인용만으로 완전 검증되지 않았다. 결론에는 약한 근거로만 사용해야 한다.
- RQ-01/RQ-03: Anthropic/Replit/Devin/allpay/Dow/Salesforce 등 vendor/customer story의 장기 품질, 재작업, 오류율, 순재무성과는 공개 원문만으로 독립 검증되지 않았다.

## Expansion으로 보존할 항목

| item | why verifier cannot resolve it | route |
| --- | --- | --- |
| 최신 Codex/Claude Code/GitHub Copilot coding agent의 동일 조직·동일 업무 net productivity | Repair Queue의 출처 대조 범위를 넘어서는 새 field experiment/telemetry 조사 필요 | Expansion Queue |
| 일반 업무 자동화의 독립 성과와 실패율 | 현재 검증 대상은 vendor recipe/customer story 보정이며, 업무별 독립 성과 데이터 발굴은 coverage gap | Expansion Queue |
| 보안/거버넌스 guardrail의 productivity tax 정량값 | 승인 지연, false positive, scanner 비용, prompt fatigue 등은 추가 telemetry/사례 조사가 필요 | Expansion Queue |
| agent-caused incident/near-miss 발생률과 손실 규모 | 현재 사고 사례 존재 여부가 아니라 발생률/대표성 문제이므로 별도 incident dataset 조사가 필요 | Expansion Queue |
| Codex/Claude Code/Copilot/Devin/Replit head-to-head task-stratified 비교 | 도구별 순위 또는 동일 task 비교는 Repair Queue 범위를 벗어난 추가 연구 | Expansion Queue |
| `업무의 소프트웨어화` 프레임의 조직 조건 | 현재는 사례 귀납 프레임이며 독립 실증 또는 조직 조건 연구가 더 필요 | Expansion Queue |
