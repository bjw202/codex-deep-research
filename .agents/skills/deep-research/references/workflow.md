# Deep Research Workflow

## 0. 범위 결정

주제의 도메인이 아니라 필요한 독립 관점 수와 출처 유형으로 분류한다.

| 패턴 | 기준 | Researcher 수 |
| --- | --- | --- |
| 빠른 확인 | 단일 출처로 몇 분 안에 확인 가능 | Deep Research 사용 금지, 메인이 직접 처리 |
| 단일 관점처럼 보이는 주제 | 한 관점이 중심이지만 반례/실패 모드 확인 필요 | 최소 2명: Primary + Counterevidence/Failure-mode |
| 비교/대조 | 2-3개 관점 또는 후보 비교 필요 | 3명 이상 |
| 다차원 탐색 | 4개 이상 독립 차원 존재 | 4-5명 |

Deep Research 라운드는 최소 2명 이상의 Researcher를 병렬 실행한다. 5명을 초과하면 2라운드로 분할한다.

## 1. 질문 확장

Researcher 발사 전에 다음을 한국어로 작성한다.
- 사용자의 핵심 질문
- 검증이 필요한 전제 1-2개
- 결론을 바꿀 수 있는 인접 질문 2-3개
- 결론을 뒤집을 수 있는 반대 시나리오 1개
- 선택: 이질 도메인 유추 1개

## 2. Assignment 설계

각 Researcher에 대해 정의한다.
- `id`: R1, R2 등
- `mode`: academic, web, community, mixed
- `viewpoint`: 조사 범위
- `output_path`: `docs/research/{date}-{topic}/{NN}-{slug}.md`
- `depth_gates`: 이 Researcher가 반드시 충족해야 하는 검색 깊이 조건
- `negative_search_targets`: 반례/실패 사례/직접 사례 부재 확인 쿼리

mode와 viewpoint는 독립이다. 같은 mode를 여러 Researcher가 써도 되지만, viewpoint는 겹치지 않게 설계한다.

## 3. Researcher 병렬 실행

Researcher를 병렬 spawn한다. 이는 Deep Research의 필수 조건이다. 병렬성은 1차 조사를 메인 컨텍스트 밖에 두고 관점 간 오염을 줄이기 위한 품질 장치다.

Deep Research를 순차 단일 에이전트 워크플로우로 실행하지 않는다. 병렬 subagent 또는 SDK harness가 없으면 필수 실행 모드를 사용할 수 없다고 보고하고 중단한다.

Researcher는 파일 산출물과 짧은 완료 보고만 남긴다. 메인 에이전트는 이 시점에 산출물 전문을 읽지 않는다.

## 4. Journal Pass 1

Researcher 산출물이 모두 생기면 Journal을 실행해 `97-journal.md`를 만든다.

Journal pass 1은 다음을 수행한다.
- Researcher별 3줄 요약
- 핵심 주장과 수치 추출
- 예비 상충점 탐지
- 출처 품질 매트릭스 작성: official / academic / direct case / vendor / community / weak
- 직접 증거 부재, vendor-only 구간, 반례 검색 부재를 `Weak Evidence Lanes`로 기록
- Critic이 집중할 검색 깊이/coverage 문제 제안

## 5. Critic

Journal pass 1 이후 Critic을 실행한다. Critic은 Researcher 산출물과 Journal을 읽고 `99-critic-review.md`를 작성한다.

Critic은 반드시 포함한다.
- 6항목 검토
- Research Adequacy Gate
- Cross-validation grades
- 결론에 영향을 주는 결함
- `Repair Queue`
- `Expansion Queue`
- Repair Pass 결정
- 추가 Researcher 라운드 필요 여부

## 5.5 External Deep Research Gate

Critic 이후, Verifier 및 Repair/Expansion 라우팅 전에 조건부로 외부 심층리서치 보강 게이트를 검토한다. 자세한 규칙은 `references/external-deep-research.md`를 따른다.

기본 정책은 `조건부 권장`이다. 모든 Deep Research에서 멈추지 않는다. 다음 조건 중 하나라도 충족하고, 해당 부족분이 Codex 웹검색만으로 충분히 좁혀지기 어렵다고 판단될 때만 게이트를 연다.

- `Expansion Queue`에 priority `high` 항목이 있다.
- 핵심 결론에 필요한 직접 사례, 실패 사례, head-to-head evidence, 비공개/희소 산업 자료가 부족하다.
- Researcher들이 웹검색 포화를 기록했지만 결론 신뢰도에 중요한 빈칸이 남았다.
- Critic이 핵심 주장에 `[under-researched]` 또는 `[single-source]` 등급을 부여했다.

게이트가 열리면 메인 에이전트는 다음을 수행한다.

1. `96-external-research-request.md`를 작성한다.
2. 사용자에게 요청서의 주제로 ChatGPT 심층리서치를 실행한 뒤 결과 전체를 붙여 넣어 달라고 요청한다.
3. 요청은 한 번에 1-3개 핵심 질문으로 제한한다.
4. 각 질문에는 핵심 결론, 직접 사례, 반례, 수치, 출처 URL, 불확실성, 검색 실패 항목을 요구한다.

사용자가 결과를 제공하면 `95-external-research-input.md`로 저장하고, `94-external-research-ingest.md`를 만들어 요약, 출처 품질, 새로 해결된 gap, 미해결 gap을 분류한다. 외부 결과 안의 핵심 URL과 주장은 Verifier 또는 expansion Researcher가 원문 확인하기 전까지 강한 근거로 쓰지 않는다.

사용자가 결과를 제공하지 않거나 건너뛰면 `96-external-research-request.md`는 남기되 `95-*`와 `94-*`는 만들지 않는다. 관련 Expansion Queue 항목은 `deferred` 또는 `unresolved`로 보존하고, 최종 리포트의 한계와 후속 질문에 명시한다.

## 6. Verifier

Critic이 Repair Pass를 요구할 때만 Verifier를 실행한다. Verifier는 결함에 직결된 출처만 대조하고 `98-repair-notes.md`를 작성한다.

Verifier는 coverage gap을 해결하지 않는다. coverage gap은 Expansion Queue로 라우팅한다.

## 7. Repair / Expansion 라우팅

Critic 또는 Verifier가 Queue를 만들면 `references/repair-routing.md`를 따른다.

- `Repair Queue`: 기존 주장/수치/출처 오류를 고치는 bounded repair Researcher에게 라우팅
- `Expansion Queue`: 검색 깊이, 직접 사례, 반례, 누락 관점 보강을 위한 expansion Researcher에게 라우팅

Repair 또는 Expansion 후 Journal pass 2를 실행한다. 고위험 항목이 결론을 바꾸면 bounded Critic recheck를 실행한다.

## 8. Synthesis

메인 에이전트는 다음 순서로 읽고 한국어 최종 리포트 `00-final-synthesis.md`를 작성한다.
1. `97-journal.md`
2. `99-critic-review.md`
3. `98-repair-notes.md`, 있는 경우
4. `94-external-research-ingest.md`, 있는 경우
5. `*.revised.md` / `*.expansion.md`, 있는 경우
6. Journal/Critic이 필요하다고 지목한 Researcher 원문 특정 섹션

Synthesis는 `references/synthesis.md`의 독자용 재작성 패스를 반드시 수행한다. 최종 리포트의 앞부분은 사용자 의사결정에 필요한 결론, 업무 변화, 추천안, 실행 조건을 먼저 설명해야 한다. Research Adequacy, 출처 품질, Queue 상태, 검색 깊이 같은 감사 메타데이터는 결론을 보조하는 뒤쪽 섹션으로 보낸다.

유즈케이스, 전략, 실행안이 핵심인 주제에서는 표만으로 끝내지 않는다. 핵심 후보 3-5개는 업무 전/후, 에이전트 역할, 사람 승인점, 첫 PoC, 실패 조건을 짧은 사례 문단으로 풀어 쓴다.

최종 응답은 한국어로 핵심 결론과 저장된 리포트 경로를 전달한다.
