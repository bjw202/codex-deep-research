# Search Policy

## 금지 도구

사용하지 않는다.
- Tavily
- Perplexity
- `search.sh`
- Tavily 또는 Perplexity를 내부 provider로 포함한 wrapper

기존 복사 지침에 위 도구가 언급되어 있으면 폐기된 지침으로 간주한다.

## 허용 검색 표면

현재 환경에서 사용 가능한 다음 수단을 사용한다.
- Codex 브라우징 / web 도구
- OpenAI Responses API `web_search`
- OpenAI 제품/API 질문의 경우 공식 Docs MCP
- 직접 URL fetch
- 사용자 제공 문서, 로컬 파일, PDF, 데이터셋, 저장소 내용

## 검색 횟수 정책

웹 검색 횟수 상한은 두지 않는다. 유료 외부 검색 도구를 쓰지 않는다는 전제에서, Researcher는 아래 깊이 게이트를 충족할 때까지 검색한다.

다만 무한 검색을 피하기 위해, 더 검색해도 새 독립 증거가 나오지 않는다고 판단되면 `검색 포화 판단` 섹션에 근거를 쓰고 멈춘다.

## 검색 깊이 게이트

각 Researcher는 자신의 viewpoint에 맞게 다음 중 적용 가능한 항목을 충족해야 한다.

### 공통 필수

- 공식/1차 출처 최소 2개
- 학술/표준/특허/기술 논문 최소 2개, 해당 분야에 존재하지 않으면 부재를 기록
- 직접 사례 또는 실험/공정 사례 최소 2개, 없으면 `직접 사례 부재`로 쿼리와 함께 기록
- 반례/실패 사례/한계 사례 최소 2개 검색
- 핵심 수치마다 원문 URL, 날짜 또는 문서 버전, 적용 조건 기록
- vendor 자료만으로 결론을 내리는 구간은 `vendor-only`로 표시
- 직접 head-to-head evidence가 없으면 `비교 직접증거 없음`을 명시

### Academic mode

우선 탐색:
- `arxiv.org`, `semanticscholar.org`, `pubmed.ncbi.nlm.nih.gov`, `ieee.org`, `dl.acm.org`, `jstor.org`, `nber.org`, `ssrn.com`, `link.springer.com`, `sciencedirect.com`, 분야별 학회/저널

증거 등급:
- Tier 1: 피어리뷰 저널, 주요 학회, 메타분석, 표준
- Tier 2: 프리프린트, 기관 보고서, 학위논문, 일반 학회
- Tier 3: 벤더 백서, 기술 블로그, 포럼, 미검증 출처

### Web mode

증거 분류:
- official: 직접 출처, 보도자료, 공식 문서, 법령, 표준
- reliable: 독립 보도, 독립 분석, 전문가 보고서
- stakeholder: 벤더, 경쟁사, 투자자, 이해관계자
- unverified: 루머, 익명 주장, 단일 약한 출처

각 핵심 주장을 Fact, Claim, Unverified 중 하나로 표시한다.

### Community mode

차단 도메인:
- `dcinside.com`
- `fmkorea.com`
- `ilbe.com`
- `yeoseongsidae.com`

전문 커뮤니티를 우선한다.
- Hacker News, Stack Overflow, 공식 포럼, GitHub issues/discussions, Product Hunt, 산업 포럼, 관련성이 명확한 Reddit subreddit

커뮤니티 증거만으로 최고 확신도를 부여하지 않는다.

## Negative Search 기록

Researcher는 다음 유형의 쿼리를 실제로 시도하고 결과를 기록한다.
- `{주제} failure`
- `{주제} defect`
- `{주제} limitation`
- `{주제} incompatible`
- `{주제} direct comparison`
- `{주제} case study`
- 한국어 주제라면 한국어 실패/불량/한계/비교/사례 쿼리도 포함

결과가 없으면 “검색했지만 직접 증거를 찾지 못함”이라고 쓰고, 이것을 결론의 불확실성에 반영한다.

## 출처 품질 매트릭스

각 Researcher 산출물에는 다음 표를 포함한다.

| 출처 유형 | 개수 | 핵심 기여 | 약점 |
| --- | ---: | --- | --- |
| official / primary |  |  |  |
| academic / standard / patent |  |  |  |
| direct case / experiment |  |  |  |
| vendor / stakeholder |  |  |  |
| community |  |  |  |
| weak / unverified |  |  |  |

## 검색 포화 판단

검색을 멈출 때는 다음을 기록한다.
- 더 검색해도 새 증거 유형이 늘지 않는 이유
- 아직 직접 증거가 부족한 항목
- 다음 라운드에서 필요한 검색 질문
