# SDK Orchestration

## 목적

이 참조는 대화형 Codex skill이 아니라 Codex SDK 또는 OpenAI Agents SDK 기반 하네스를 구현할 때만 사용한다.

## 권장 제어 모델

manager-owned parallel workflow를 사용한다. Manager가 소유한다.
- research plan
- task creation
- parallel execution
- artifact paths
- repair queue routing
- expansion queue routing
- final synthesis request

Specialist는 bounded output만 소유한다.
- Researcher: 하나의 관점 산출물
- Journal: `97-journal.md`
- Critic: `99-critic-review.md`
- Verifier: `98-repair-notes.md`
- Repair Researcher: `*.revised.md`
- Expansion Researcher: `*.expansion.md`

순차 단일 에이전트 실행은 Deep Research 구현이 아니다. 빠른 확인 작업에서만 이 스킬 밖에서 허용한다.

## Agents SDK 패턴

이 워크플로우에는 "agents as tools" 패턴을 우선한다. 최종 답변 소유권은 manager가 유지하고, specialist를 bounded capability로 호출한다.

Researcher, Critic, Verifier에게 전체 워크플로우 ownership을 handoff하지 않는다.

## 상태

단계 사이에 다음 상태를 보존한다.

```json
{
  "topic": "...",
  "workspace": "docs/research/YYYY-MM-DD-topic/",
  "assignments": [],
  "artifacts": {
    "researcher_outputs": [],
    "journal": null,
    "critic": null,
    "verifier": null,
    "revisions": [],
    "expansions": []
  },
  "repair_queue": [],
  "expansion_queue": [],
  "repair_status": [],
  "adequacy_gate": {}
}
```

## Routing Algorithm

```text
run researchers in parallel
run journal pass 1
run critic

if critic.expansion_queue not empty:
  spawn expansion researchers
  run journal pass 2
  run bounded critic recheck

if critic.repair_queue not empty:
  spawn repair researchers or verifier as appropriate
  run journal pass 2
  run bounded critic recheck

if adequacy gate passes:
  run synthesis
else:
  report unresolved research gaps
```

## 도구 정책

하네스는 같은 검색 제한을 강제한다.
- Tavily 금지
- Perplexity 금지
- `search.sh` 금지
- OpenAI `web_search`, Codex browsing, Docs MCP, 직접 source fetch, 사용자 제공 파일만 허용

웹 검색 횟수 상한은 두지 않는다. 대신 검색 깊이 게이트와 검색 포화 판단을 저장한다.

## 실패 처리

- Researcher가 빈 산출물을 만들면 해당 assignment를 1회 재실행한다.
- Journal이 실패하면 같은 역할의 새 Journal을 실행한다. 메인이 직접 Journal을 대체하지 않는다.
- Critic이 실패하면 Synthesis를 중단한다.
- Verifier가 출처에 접근하지 못하면 추측하지 말고 inaccessible로 기록한다.
- thread 한도에 걸리면 완료된 agent를 close한 뒤 다음 단계 agent를 실행한다.
