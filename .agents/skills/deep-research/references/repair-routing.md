# Repair And Expansion Routing

## 목적

Critic과 Verifier가 writer가 되지 않도록 결함과 추가 조사 필요성을 라우팅한다. 메인 에이전트는 router로 남는다.

## Queue 구분

`Repair Queue`:
- 기존 산출물의 수치, 출처, 과잉 주장, 상충 해석을 수정한다.
- 범위를 넓히지 않는다.

`Expansion Queue`:
- 검색 깊이 부족, 직접 사례 부재, 반례 검색 부족, 누락 관점을 보강한다.
- 새 Researcher를 병렬 또는 추가 라운드로 발사한다.

## Repair 라우팅 규칙

각 Repair Queue 항목에 대해:
1. 원 Researcher thread가 살아 있으면 해당 Researcher에게 보낸다.
2. 없으면 bounded repair Researcher를 새로 spawn한다.
3. 지정된 repair row만 수정한다.
4. `*.revised.md` 또는 `## Corrections`를 만들게 한다.

## Expansion 라우팅 규칙

Expansion 라우팅 전에 `references/external-deep-research.md`의 External Deep Research Gate를 검토한다. Gate가 열린 경우, 사용자 제공 외부 리서치 결과 또는 사용자의 skip/defer 결정을 반영한 뒤 Expansion Queue 항목을 `expanded`, `deferred`, 또는 `unresolved`로 처리한다.

각 Expansion Queue 항목에 대해:
1. 기존 Researcher에게 보내지 말고 새 expansion Researcher를 우선한다.
2. 누락 증거 유형과 depth gate를 명시한다.
3. 기존 결론을 보강하거나 반박하는 독립 산출물 `NN-expansion-*.md`를 만들게 한다.
4. Expansion 후 Journal pass 2와 bounded Critic recheck를 수행한다.

## Repair Prompt Template

```text
이전 Researcher 산출물을 제한적으로 수정하라.

Target file: {target_file}
Repair rows:
{repair_rows}

규칙:
- repair row에 직접 연결된 주장만 수정한다.
- 원 출처 맥락을 보존한다.
- 불확실성을 명시한다.
- 범위를 확장하지 않는다.
- {original-name}.revised.md로 저장한다.
```

## Expansion Prompt Template

```text
Deep Research expansion Researcher로 동작하라.

Missing evidence:
{missing_evidence}

Required depth gate:
{required_depth_gate}

규칙:
- 기존 산출물을 정당화하려고 하지 말고 독립적으로 조사한다.
- 직접 사례, 반례, 실패 사례, head-to-head evidence를 우선한다.
- 찾지 못한 직접 증거도 검색 로그와 함께 기록한다.
- 한국어 Markdown으로 {output_path}에 저장한다.
```

## 후속 처리

Repair 또는 Expansion 후:
1. External Deep Research Gate 결과가 있으면 `94-external-research-ingest.md` 또는 deferred/unresolved 상태를 Journal에 반영
2. Journal pass 2 실행
3. high priority 항목이 결론을 바꾸면 bounded Critic recheck 실행
4. Research Adequacy Gate가 통과된 뒤 Synthesis 실행

## 상태값

- `routed`
- `repaired`
- `expanded`
- `verified`
- `external-requested`
- `external-ingested`
- `unresolved`
- `deferred`
