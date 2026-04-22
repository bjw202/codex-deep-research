# External Deep Research Gate

## 목적

Codex 웹검색 기반 Deep Research가 검색 포화에 도달했지만 핵심 결론에 중요한 coverage gap이 남은 경우, 사용자에게 ChatGPT 심층리서치를 별도로 실행하도록 요청하고 그 결과를 워크플로우에 안전하게 반영한다.

이 단계는 Researcher를 대체하지 않는다. 사용자 제공 외부 리서치는 추가 입력이며, 원문 URL 확인 전에는 강한 근거로 승격하지 않는다.

## 위치

Critic 이후, Verifier 및 Repair/Expansion 라우팅 전에 실행 여부를 판단한다.

```text
Journal Pass 1 -> Critic -> External Deep Research Gate -> Verifier / Repair / Expansion -> Journal Pass 2 -> Synthesis
```

## 발동 조건

기본 정책은 `조건부 권장`이다. 모든 리서치에서 멈추지 않는다.

다음 조건 중 하나라도 충족하고, 해당 부족분이 Codex 웹검색만으로 충분히 좁혀지기 어렵다고 판단될 때 게이트를 연다.

- `Expansion Queue`에 priority `high` 항목이 있다.
- 핵심 결론에 필요한 직접 사례, 실패 사례, head-to-head evidence, 비공개/희소 산업 자료가 부족하다.
- Researcher들이 웹검색 포화를 기록했지만 결론 신뢰도에 중요한 빈칸이 남았다.
- Critic이 핵심 주장에 `[under-researched]` 또는 `[single-source]` 등급을 부여했다.

게이트를 열지 않는 경우:

- 부족분이 final synthesis의 한계로 명시해도 되는 낮은 중요도의 gap이다.
- 추가 Researcher가 공개 웹검색만으로 충분히 해결할 수 있다.
- 사용자가 처음부터 빠른 결과를 명시했고, 게이트가 리포트 목적을 과도하게 지연시킨다.

## 산출물

게이트가 열리면 `96-external-research-request.md`를 작성한다.

사용자가 결과를 제공하면 다음 파일을 만든다.

- `95-external-research-input.md`: 사용자가 붙여 넣은 ChatGPT 심층리서치 결과 원문
- `94-external-research-ingest.md`: 외부 결과의 요약, 출처 품질, 해결된 gap, 미해결 gap, 검증 필요 URL

사용자가 결과를 제공하지 않거나 건너뛰면 `95-*`와 `94-*`는 만들지 않는다. `96-*`는 남겨 후속 조사 요청서로 보존한다.

## 요청서 작성 규칙

`96-external-research-request.md`는 한 번에 1-3개 핵심 질문만 포함한다. Critic의 high-priority Expansion Queue에서 결론 영향이 큰 순서로 고른다.

각 질문에는 다음을 요구한다.

- 핵심 결론
- 직접 사례
- 실패 사례 또는 반례
- 정량 수치
- 원문 URL
- 불확실성
- 검색했지만 찾지 못한 항목

## 요청서 템플릿

```markdown
# ChatGPT 심층리서치 요청

## 왜 필요한가

현재 Codex 웹서치 기반 Deep Research에서 아래 증거 부족이 남았습니다. 이 항목은 결론 신뢰도에 영향을 주지만, 일반 웹검색만으로는 직접 사례/반례/수치가 충분하지 않았습니다.

## 요청할 주제

1. {Critic Expansion Queue의 high-priority missing_evidence}

## ChatGPT 심층리서치에 입력할 프롬프트

다음 주제에 대해 심층리서치를 수행해 주세요.

- 핵심 질문: ...
- 반드시 찾을 증거: 직접 사례, 실패 사례, 반례, 정량 수치, 원문 URL
- 구분할 출처 유형: official, academic/standard, direct case, vendor/stakeholder, community, weak
- 반드시 포함할 한계: 증거 부족, vendor-only 구간, 직접 비교 부재
- 출력 형식: Markdown 표와 요약

## 사용자가 Codex에 붙여 넣을 내용

ChatGPT 심층리서치 결과 전체를 그대로 붙여 넣어 주세요. 가능하면 출처 URL이 포함된 원문 형식을 유지해 주세요.
```

## 사용자 응답 처리

사용자가 결과를 제공하면 메인 에이전트는 사용자의 입력을 `95-external-research-input.md`로 저장한다.

그 다음 Journal 또는 bounded Researcher에게 `94-external-research-ingest.md`를 작성하게 한다. Ingest는 검색하지 않아도 되며, 필요한 경우 핵심 URL의 원문 확인은 Verifier 또는 expansion Researcher에게 라우팅한다.

`94-external-research-ingest.md`는 사용자가 외부 리서치 결과가 실제로 무엇을 보강했는지 쉽게 읽을 수 있어야 한다. 작성 전 `references/report-writing.md`를 따르고, 출처 품질 표보다 먼저 "이번 외부 입력으로 달라진 점"을 쉬운 말로 쓴다.

`94-external-research-ingest.md`에는 다음을 포함한다.

```markdown
# External Research Ingest - {주제}

## 입력 요약

## 이번 입력으로 달라진 점

## 해결된 gap
| gap | 외부 결과의 기여 | 출처 URL | 신뢰도 | 검증 필요 여부 |
| --- | --- | --- | --- | --- |

## 출처 품질
| 출처 유형 | 개수 | 핵심 기여 | 약점 |
| --- | ---: | --- | --- |

## 기존 산출물과의 상충
| 항목 | 기존 주장 | 외부 결과 | 처리 |
| --- | --- | --- | --- |

## 원문 확인 필요 항목
| 주장 | URL | 필요한 확인 |
| --- | --- | --- |

## 남은 미해결 gap
```

## 신뢰도 규칙

- ChatGPT 심층리서치 결과는 `user-provided external research`로 분류한다.
- 출처 URL이 없는 요약은 `weak/user-provided`로만 반영한다.
- 최종 리포트에서 강한 주장으로 쓰려면 다음 중 하나가 필요하다.
  - 결과 안의 원문 URL을 Verifier가 확인했다.
  - expansion Researcher가 해당 출처를 독립적으로 재검토했다.
  - 기존 Researcher 산출물과 2개 이상 독립 출처 채널에서 교차 확인됐다.
- 외부 결과가 기존 결론과 충돌하면 삭제하지 않는다. Journal과 Synthesis의 상충점에 보존한다.
- 외부 결과의 큰 수치가 vendor/customer story라면 `출처 존재`와 `효과 크기/ROI 확신도`를 분리한다.

## Graceful Resume

사용자가 ChatGPT 심층리서치 결과를 제공하지 않거나 건너뛰겠다고 하면 워크플로우를 중단하지 않는다.

메인 에이전트는 다음을 수행한다.

1. `96-external-research-request.md`를 후속 조사 요청서로 보존한다.
2. 관련 Expansion Queue 항목을 `deferred` 또는 `unresolved`로 표시한다.
3. Journal Pass 2에 External Deep Research Gate 상태를 기록한다.
4. Synthesis의 `한계`, `후속 질문`, `출처와 검색 깊이 요약`에 추가 ChatGPT 심층리서치 권장 항목으로 명시한다.

## 하드 규칙

- Codex가 ChatGPT Deep Research 기능을 직접 실행할 수 있다고 가정하지 않는다.
- 사용자에게 맡긴 외부 리서치를 공식/학술/직접 사례와 같은 등급으로 취급하지 않는다.
- 외부 결과를 받았다는 이유만으로 Research Adequacy Gate를 자동 통과시키지 않는다.
- 기존 금지 도구 정책을 유지한다. Tavily, Perplexity, `search.sh`, 또는 해당 wrapper는 사용하지 않는다.
