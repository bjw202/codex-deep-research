---
name: deep-research
description: 복합 주제의 심층 조사, 비교 분석, 기술/시장/학술/커뮤니티 리서치, 근거 기반 의사결정 리포트를 병렬 에이전트로 수행하고, 중간 산출물과 최종 종합 리포트를 독자가 읽기 쉬운 상세 리포트로 작성한다. 사용자가 deep research, 딥리서치, 리서치, 조사, 분석, 다각도 검토, 근거 기반 보고서, 병렬 Researcher, Journal, Critic, Verifier, Synthesis를 요청할 때 사용한다. 단일 출처로 충분한 빠른 사실 확인에는 사용하지 않는다.
---

# Deep Research

## 핵심 원칙

메인 에이전트는 오케스트레이션, 라우팅, 최종 종합에 집중한다. 메인 에이전트가 직접 광범위한 1차 조사를 수행하거나, Journal과 Critic이 압축하기 전에 Researcher 산출물을 전부 정독하지 않는다.

이 워크플로우는 다음 이유로 존재한다.
- Researcher가 1차 조사를 소유한다.
- Journal이 메인 컨텍스트를 보호하고 상충점과 출처 품질을 구조화한다.
- Critic이 주장, 검색 깊이, 출처 직접성, 결함, 확장 필요성을 평가한다.
- Verifier가 결함에 직결된 출처만 대조한다.
- 메인 에이전트는 구조화된 중간 산출물로 한국어 최종 리포트를 작성한다.

## 언어 규칙

스킬 지시, 중간 산출물, 최종 리포트는 기본적으로 한국어로 작성한다. 사용자가 다른 언어를 명시한 경우에만 예외로 한다. 고유명사, 논문 제목, 제품명, 표준명, 원문 인용은 원어를 유지할 수 있다.

## 리포트 작성 원칙

모든 중간 산출물은 감사 로그이면서 동시에 사용자가 직접 읽는 상세 리포트다. 최종 Synthesis는 감사 로그가 아니라 의사결정 문서다. Researcher, Journal, Critic, Verifier, External Ingest, Synthesis는 모두 `references/report-writing.md`의 독자 중심 문체 규칙을 따른다. 정확성을 위해 필요한 메타데이터는 보존하되, 최종 리포트 앞부분에는 결론, 업무 변화, 추천안, 실행 조건을 먼저 설명한다.

## 로드 순서

필요할 때만 참조 파일을 읽는다.
- 전체 실행 흐름: `references/workflow.md`
- 모든 리포트 산출물 작성 전: `references/report-writing.md`
- 검색 정책과 깊이 기준: `references/search-policy.md`
- Researcher 발사 전: `references/researcher.md`
- Journal 실행 전: `references/journal.md`
- Critic 실행 전: `references/critic.md`
- Critic 이후 외부 심층리서치 보강이 필요할 때: `references/external-deep-research.md`
- Verifier는 Critic이 Repair Pass를 요구할 때만: `references/verifier.md`
- Repair/Expansion 라우팅 필요 시: `references/repair-routing.md`
- 최종 리포트 작성 전: `references/synthesis.md`
- Codex SDK 또는 OpenAI Agents SDK 하네스 구현 시에만: `references/sdk-orchestration.md`

## 실행 규칙

Deep Research는 병렬 에이전트 실행이 필수다. `$deep-research`, `deep research`, `딥리서치`, 또는 이 스킬 사용 요청은 역할이 분리된 Researcher 에이전트를 병렬로 spawn하라는 허가이자 요구로 해석한다.

Deep Research를 순차 단일 에이전트 워크플로우로 실행하지 않는다. 순차 fallback은 메인 컨텍스트를 오염시키고 리포트 품질을 떨어뜨린다. subagent 또는 SDK harness가 사용할 수 없으면 Deep Research를 필수 모드로 실행할 수 없다고 보고하고 중단한다.

subagent를 사용할 때는 가능한 경우 프로젝트 커스텀 에이전트를 우선한다.
- `research_researcher`
- `research_journal`
- `research_critic`
- `research_verifier`

커스텀 에이전트가 없고 generic subagent만 가능하면, `default` 또는 `worker` 에이전트에 관련 참조 파일을 프롬프트로 삽입한다. 역할 분리는 반드시 유지한다.

독립 앱이나 CLI 하네스에서는 동일한 역할 경계를 코드로 구현한다. `references/sdk-orchestration.md`를 따른다.

## 필수 산출물

리서치 작업공간을 만든다.

```text
docs/research/{YYYY-MM-DD}-{topic-slug}/
```

표준 파일:
- `01-*` to `89-*`: Researcher 산출물
- `94-external-research-ingest.md`: 사용자 제공 ChatGPT 심층리서치 결과의 요약/분류, 있는 경우만
- `95-external-research-input.md`: 사용자가 붙여 넣은 ChatGPT 심층리서치 결과, 있는 경우만
- `96-external-research-request.md`: 사용자에게 전달할 ChatGPT 심층리서치 요청서, 필요한 경우만
- `97-journal.md`: Journal 요약, 상충점, 출처 품질, 검색 깊이 메타데이터
- `98-repair-notes.md`: Verifier 출처 대조 노트, 필요한 경우만
- `99-critic-review.md`: Critic 검토, Research Adequacy Gate, Repair Queue, Expansion Queue
- `00-final-synthesis.md`: 한국어 최종 리포트

## 검색 제한과 깊이

Tavily, Perplexity, `search.sh`, 또는 이들을 포함한 wrapper는 사용하지 않는다. Codex 브라우징, OpenAI Responses API `web_search`, 공식 Docs MCP, 직접 URL fetch, 사용자 제공 문서/파일만 사용한다.

웹 검색 횟수 상한은 두지 않는다. 외부 유료 검색 도구를 쓰지 않기 때문이다. 대신 Researcher는 `references/search-policy.md`의 검색 깊이 게이트를 충족할 때까지 검색하고, 충족하지 못한 항목은 명시적으로 `증거 부족`으로 기록한다.

커뮤니티 조사에서 차단할 도메인:
- `dcinside.com`
- `fmkorea.com`
- `ilbe.com`
- `yeoseongsidae.com`

## Repair / Expansion 규칙

Critic과 Verifier는 Researcher 산출물을 직접 다시 쓰지 않는다. Critic은 결함은 `Repair Queue`, 검색 깊이/coverage 부족은 `Expansion Queue`에 기록한다.

메인 에이전트는 각 Queue 항목을 원 Researcher 또는 bounded repair/expansion Researcher에게 라우팅한다. 원본을 조용히 덮어쓰지 말고 `*.revised.md`, `*.expansion.md`, 또는 명시적 `## Corrections` 섹션을 만든다.

## External Deep Research Gate

Critic 이후, Repair/Expansion 라우팅 전에 조건부로 ChatGPT 심층리서치 보강 게이트를 검토한다. 기본 정책은 `조건부 권장`이다. 모든 리서치에서 멈추지 않고, Critic이 high-priority coverage gap을 남겼으며 그 부족분이 Codex 웹검색만으로 충분히 좁혀지기 어렵다고 판단될 때만 사용자에게 ChatGPT 심층리서치 수행을 요청한다.

이 게이트가 열리면 `references/external-deep-research.md`를 따른다. 사용자가 결과를 제공하면 사용자 제공 외부 리서치 산출물로 저장/분류하고, 원문 URL 확인 전에는 강한 근거로 승격하지 않는다. 사용자가 건너뛰거나 결과를 제공하지 않으면 워크플로우를 중단하지 않고 해당 gap을 `deferred` 또는 `unresolved`로 보존한 뒤 최종 리포트의 한계와 후속 질문에 반영한다.
