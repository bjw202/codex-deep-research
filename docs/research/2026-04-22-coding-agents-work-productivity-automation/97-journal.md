# 리서치 저널 - 코딩 에이전트의 업무생산성 향상과 혁신/자동화

**Date**: 2026-04-22  
**Workspace**: docs/research/2026-04-22-coding-agents-work-productivity-automation/  
**Journal Pass**: Pass 2 - Critic/Verifier/Repair 반영  
**입력 산출물**: `97-journal.md`, `99-critic-review.md`, `98-repair-notes.md`, `01-productivity-evidence.md`, `02-enterprise-cases.md`, `03-workflow-patterns.md`, `04-risks-governance.md`, `05-future-impact.md`  
**검색 수행**: Journal은 검색하지 않았고, 지정 산출물만 읽었다.

## 1. 리서치 설계

주제는 Codex, Claude Code, GitHub Copilot, Cursor, Devin, Replit Agent 등 코딩 에이전트를 업무생산성 향상과 혁신/자동화에 활용하는 사례, 임팩트, 발전 방향이다.

Researcher 배치는 5개 관점으로 나뉜다.

| Researcher | 파일 | 관점 | 핵심 역할 |
| --- | --- | --- | --- |
| R1 | `01-productivity-evidence.md` | 측정된 생산성/업무 성과 근거 | 실험, RCT, 현장 연구, 벤치마크 신뢰성, 반례를 정리 |
| R2 | `02-enterprise-cases.md` | 실제 기업/팀 사례 | Anthropic, OpenAI, GitHub, Devin, Replit, Cursor 등 공개 사례와 실패 사례를 분리 |
| R3 | `03-workflow-patterns.md` | 업무 플로우/자동화 패턴 | 코드 외 문서, 슬라이드, 데이터, QA, inbox, issue-to-PR 등 반복 가능한 패턴 구조화 |
| R4 | `04-risks-governance.md` | 리스크, 실패 모드, governance | prompt injection, excessive agency, data exfiltration, supply chain, 감사/권한 통제 검토 |
| R5 | `05-future-impact.md` | 발전 방향과 임팩트 모델 | 1-3년 제품 방향, 조직 구조, Agentic ROI, AI-native 운영체계 가설 검토 |

Pass 2의 목적은 최종 진실 판단이 아니라 Critic과 Repair Notes가 확인한 결함, 보정된 출처 품질, 남은 상충점, Synthesis에서 사용할 문장 강도를 구조화하는 것이다.

## 2. Researcher 요약

### R1 - 측정된 생산성/업무 성과 근거

짧고 명확한 코딩 과제, 고객지원, 컨설팅형 초안/분석 업무에서는 생산성 개선 근거가 비교적 강하게 제시됐다.  
반대로 METR RCT와 DORA 2024는 숙련자·실제 저장소·릴리스 안정성 축에서 AI가 느리게 하거나 안정성을 악화시킬 수 있음을 제시했다.  
벤치마크 점수는 현장 ROI의 충분조건이 아니며, 내부 과제 샘플과 workflow redesign 기반 측정이 필요하다는 메타 결론을 제안했다.

### R2 - 실제 기업/팀 사례

Anthropic 내부 법무/마케팅/디자인, Replit UKG, Devin Nubank 등은 반복 업무를 코드화된 워크플로우와 API/MCP/PR/스케줄러로 재구성한 사례로 정리됐다.  
성과 수치는 2시간에서 15분, 10배, 8-12배, 20배, 400% 등 크지만 대부분 vendor-only 또는 이해관계자 자료다.  
Answer.AI의 Devin 실패율, Replit production DB 삭제, AI IDE 보안 취약점은 자율성과 권한 확대가 운영 리스크로 전환될 수 있음을 보여준다.

### R3 - 업무 플로우/자동화 패턴

코딩 에이전트의 업무 확장은 텍스트 생성보다 파일, 코드, 데이터, 브라우저 동작을 검증 가능한 산출물로 다루는 구조에서 강점이 있다고 정리됐다.  
핵심 패턴은 의도 입력, 컨텍스트 수집, 산출물 생성, 자동 검증, 사람 승인, 반복 업무의 skill/workflow 저장이다.  
완전 자율보다 PR, draft, report, run history, permission prompt 같은 bounded autonomy가 현실적이라는 제품 문서와 표준 근거를 모았다.

### R4 - 리스크, 실패 모드, governance

핵심 위험은 권한 있는 실행 환경, 신뢰할 수 없는 입력, 외부 송신 경로가 동시에 열리는 조합으로 정리됐다.  
Codex, Claude Code, Copilot 문서와 NIST/NCSC/OWASP는 인터넷 제한, 권한 승인, 방화벽, secret scanning, 감사로그 등 구조적 통제를 요구한다.  
Replit DB 삭제, CamoLeak, MCP/tool poisoning, package hallucination 사례는 생산성 논의에 검증 비용과 tail risk를 포함해야 함을 뒷받침한다.

### R5 - 발전 방향과 임팩트 모델

제품 방향은 IDE 보조에서 Slack/GitHub/문서/컴퓨터 조작, 장기 실행, 기억, tool use, multi-agent, enterprise governance로 이동한다고 정리됐다.  
임팩트 모델은 개인 증강, 작업 패키지 위임, 워크플로 자동화, AI-native 운영체계의 4단계로 제안됐다.  
METR, Gartner, MIT NANDA 등은 agent washing, ROI 부재, workflow integration gap, 숙련 개발자 slowdown을 주요 반례로 제시한다.

## 3. 핵심 주장과 수치

| 주장 | Researcher | 확신도 | 메모 |
| --- | --- | --- | --- |
| GitHub Copilot은 짧고 독립적인 JavaScript HTTP server 과제에서 완료 시간을 55.8% 줄였다. | R1 | 높음 | academic + GitHub 공식. 단일 greenfield 과제라 일반화 제한 |
| Microsoft/Accenture/Fortune 100 현장 RCT 통합에서 완료 작업 수가 26.08% 증가했다. | R1 | 중상 | 4,867명 통합. 낮은 채택률, ITT 비유의 구간, 산출량 중심 지표 주의 |
| 고객지원 현장 연구에서 해결 건수/시간이 약 13.8-15% 증가했고 저숙련자 효과가 더 컸다. | R1, R5 | 높음 | QJE/NBER 계열. 코딩 외 반복 지식업무 확장 근거 |
| BCG 컨설턴트 실험은 frontier 안 과제에서 속도 25%+, 품질 40%+, 완료 과제 12%+ 개선을 보고했다. | R1 | 높음 | frontier 밖 과제에서는 정답 가능성이 19% 낮아진 반례도 같은 연구에 있음 |
| METR 2025 RCT는 숙련 OSS 개발자 16명, 실제 작업 246개에서 AI 허용 시 완료 시간이 19% 증가했다고 보고했다. | R1, R4, R5 | 높음~중상 | 복잡한 기존 코드베이스와 검증 비용의 핵심 반례 |
| DORA 2024는 AI 채택 25% 증가와 문서 품질 7.5%, 코드 품질 3.4%, 리뷰 속도 3.1% 개선, throughput 1.5% 감소, stability 7.2% 감소의 연관을 보고했다. | R1 | 중상 | survey/correlation. 개인 생산성 개선과 delivery 안정성 악화 가능성을 동시에 제시 |
| Anthropic 성장마케팅 사례는 광고 카피 생성 2시간에서 15분, Figma 대량 변형 10배 개선을 주장한다. | R2 | 출처 존재 높음 / 효과 크기 중간 이하 | official/vendor-only. 독립 검증, 장기 품질, 오류율 부족 |
| Anthropic 법무팀은 마케팅 리뷰 turnaround가 2-3일에서 24시간으로 감소했다고 주장한다. | R2 | 출처 존재 높음 / 효과 크기 중간 이하 | official/vendor-only. 장기 품질/오류율 미상 |
| Devin/Nubank 사례는 일부 마이그레이션 범위에서 8-12배 엔지니어링 시간 효율, 20배 비용 절감을 주장한다. | R2 | 출처 존재 중간 / 효과 크기 낮음~중간 | vendor/customer story. 범위와 품질 보정 필요 |
| Answer.AI의 Devin hands-on은 20개 작업 중 14개 실패, 3개 성공, 3개 불명확을 보고했다. | R2 | 높음 | 독립 hands-on이지만 표본과 과제 선택 제한 |
| Replit/UKG 사례는 AI 프로토타입 피드백 수집 능력 400% 증가를 주장한다. | R2 | 출처 존재 중간 / 효과 크기 낮음~중간 | vendor/customer story. 검증된 재무성과 아님 |
| Block/goose 사례는 4,000명 내부 사용과 엔지니어 주당 8-10시간 절감 사례를 제시한다. | R3 | 중상 | vendor customer case. 독립 감사 제한 |
| Copilot 보안 연구는 보안 관련 프롬프트에서 약 40% 취약 코드, replication은 Python 취약 suggestion 27.25%를 보고했다. | R4 | 중상 | AI 생성 코드 검증 비용 근거 |
| NIST CAISI는 AgentDojo 기반 반복 공격에서 평균 attack success가 57%에서 80%로 상승했다고 보고했다. | R4 | 높음 | agent hijacking 평가에서 반복 공격 고려 필요 |
| AgentDojo detector 방어는 attack success를 8%로 낮춘 사례를 보고했다. | R4 | 높음 | 통제가 불가능한 것이 아니라 utility/security trade-off가 있다는 근거 |
| Gartner는 2027년 말까지 agentic AI project 40% 이상 취소를 예측했다. | R5 | 중상 | analyst forecast. agent washing/ROI 부족 반례 |
| MIT NANDA 계열 자료는 GenAI 투자 상당수가 zero return이며 5% 수준만 production value를 낸다는 주장을 제시했다. | R5 | 낮음~중 | mirror/언론 재인용 기반 반례 신호. 원 배포 경로·방법론·정의 검증 필요 |
| Microsoft Work Trend Index는 리더 81%가 12-18개월 내 에이전트를 AI 전략에 중등도 이상 통합할 것으로 본다고 보고했다. | R5 | 중 | vendor survey. 실제 손익 효과와 분리 필요 |

## 4. 출처 품질 매트릭스

| Researcher | official/primary | academic/standard/patent | direct case/experiment | vendor/stakeholder | weak/unverified | 비고 |
| --- | ---: | ---: | ---: | ---: | ---: | --- |
| R1 | 5 | 9 | 7 | 4 | 0 | 실험·RCT·학술 근거가 강하나 2026년 Codex/Claude Code 자체 장기 RCT는 부족 |
| R2 | 7 | 3 | 8 | 8 | 4 | 실제 사례 풍부. 성과 수치 상당수가 vendor-only이고 커뮤니티 증거 6건 별도 존재 |
| R3 | 17 | 8 | 4 | 10 | 2 | Codex workflow examples는 direct case가 아니라 official product recipe/documentation으로 보정. 일반 업무 자동화의 독립 대규모 성과 데이터는 약함 |
| R4 | 9 | 8 | 7 | 5 | 2 | 보안/거버넌스 출처 강함. 공개 사고 발생률과 guardrail 운영 수치는 부족 |
| R5 | 10 | 7 | 6 | 8 | 2 | 로드맵/미래 방향 공식 근거 강함. 장기 조직 패널과 head-to-head field experiment 부족 |
| 통합 단순 합계 | 48 | 35 | 32 | 35 | 10 | 범주 정의가 Researcher별로 약간 달라 단순 비교용이 아니라 coverage 신호로만 사용 |

추가 메타 관찰:

| 항목 | 관찰 |
| --- | --- |
| 강한 축 | 공식 제품 문서, 보안 표준, 단기 실험, 고객지원/컨설팅 field study, 일부 직접 incident |
| 중간 축 | 기업 고객 사례, vendor-reported ROI의 출처 존재, 2025-2026 arXiv/working paper, analyst forecast |
| 약한 축 | 커뮤니티 사용담, vendor 홈페이지 효과 크기, 언론이 임원 발언을 재인용한 수치, mirror PDF 기반 보고서 |
| 결핍 축 | Codex/Claude Code 최신 버전의 장기 기업 내부 RCT, 일반 업무 산출물 자동화의 독립 성과 데이터, agent-caused incident 공개 통계 |

## 5. 약한 증거 구간

| 항목 | 약한 이유 | 필요한 추가 조사 |
| --- | --- | --- |
| Codex/Claude Code 최신 버전의 실제 기업 ROI | 공식 로드맵과 고객 인용은 있으나 통제군 있는 장기 현장 연구가 부족 | 동일 조직·동일 업무에서 stepped rollout 또는 RCT, review/rework/incident 포함 측정 |
| 비개발 업무 자동화 성과 | 마케팅, 법무, FP&A, 슬라이드, inbox 사례는 vendor-only나 커뮤니티 비중이 큼 | 업무별 샘플 20-50개 이상의 성공률, 검토시간, 오류율, 재사용률 측정 |
| Devin, Replit, Agentforce 등 큰 배수의 성과 수치 | 고객/벤더 발표 중심이고 품질 보정, 범위, 실패율이 불명확 | 원자료, 대조군, baseline 정의, 유지보수/rollback 비용 확인 |
| 일반 업무 산출물의 실패/사고율 | 코드/PR/보안 incident는 일부 있으나 슬라이드·이메일·스프레드시트 자동화 실패 데이터는 일화적 | 조직 내부 near miss, false send, wrong report, spreadsheet error 로그 수집 |
| Guardrail의 운영 비용 | 네트워크 차단, approval, scanner, detector의 false positive, latency, prompt fatigue 수치 부족 | vendor별 guardrail benchmark와 운영 telemetry |
| Agentic ROI 공식 | 개념은 유용하나 실제 항목별 가중치와 측정 방법이 조직별로 다름 | 비용 항목 표준화, risk-adjusted throughput, external spend 절감 검증 |
| MIT NANDA 95% zero return 주장 | mirror PDF/언론 재인용과 방법론 세부 검증 필요. 강한 실증 근거가 아니라 반례 신호로만 유지 | 원 배포 경로, 표본, 정의, 재현 가능한 데이터 확인 |
| Gartner 40% 취소 전망 | 예측성 analyst claim이며 실측치가 아님 | 이후 실제 취소율, 취소 원인, agent washing 정의 추적 |
| MCP/tool layer 보안 논문 | 2026 preprint 비중이 높고 제품 구현이 빠르게 변함 | peer review, CVE/패치 상태, 실제 exploit 빈도 확인 |
| AI-native 운영체계/Frontier Firm | 방향성 가설은 강하지만 장기 패널 데이터가 부족 | multi-agent adoption 전후 조직 구조, headcount, cycle time, 품질 지표 추적 |

## 6. 예비 상충점

| 항목 | A | B | 상충 유형 | Critic focus |
| --- | --- | --- | --- | --- |
| 코딩 생산성 효과 | Copilot 단기 실험 55.8% 빠름, 현장 RCT 완료 작업 +26.08% | METR 실제 OSS 작업 19% 느림 | 과제 구조·경험 수준·검증 비용 차이 | 어떤 업무 조건에서 양/음 효과가 갈리는지 분해 |
| 개인 생산성 vs delivery 성과 | DORA: 문서/코드 품질, 리뷰 속도 개선 | DORA: throughput -1.5%, stability -7.2% | 개인/팀/운영 지표 불일치 | 최종 리포트 KPI를 개인 속도에 고정하지 않도록 검토 |
| vendor 고객 사례 vs 독립 hands-on | Devin/Nubank 8-12배, 20배 비용 절감 | Answer.AI Devin 20개 중 14 실패 | 성공 편향과 과제 선택 차이 | vendor-only 수치의 표현 강도 조정 |
| 자율 에이전트 방향 vs bounded autonomy | 제품 로드맵은 long-horizon, automation, computer use 강조 | 보안 문서와 incident는 PR/draft/approval/read-only 강조 | 제품 비전과 운영 안전성 긴장 | "자율화"를 권한 tier와 승인 체계로 재정의 |
| 비개발자 업무 자동화 | Replit/Claude Code는 비기술 사용자와 법무/마케팅 자동화 사례 제시 | 성공 사례가 실제로는 API, Git, MCP, 테스트, 스크립트 등 소프트웨어화에 의존 | 비개발 업무와 소프트웨어화의 경계 | "자연어만으로 업무 완결" 주장 방지 |
| 벤치마크/모델 성능 vs governance readiness | GPT/Codex/Claude 로드맵은 장기 실행과 성능 향상 강조 | AgentDojo, NIST, OWASP는 권한·데이터·egress 통제 없이는 위험하다고 지적 | capability와 deployability 차이 | 벤치마크 점수를 ROI/도입 승인 근거로 쓰지 않도록 검토 |
| 통제 효과 vs 생산성 마찰 | AgentDojo detector, Codex allowlist, Claude auto mode, GitHub firewall은 위험을 낮춤 | 승인, false positive, 제한 네트워크, scanner가 latency와 우회 행동을 만들 수 있음 | 보안-생산성 trade-off | guardrail 비용이 ROI에 포함됐는지 확인 |
| 미래 낙관론 vs ROI 실패론 | Microsoft Work Trend Index, OpenAI/Anthropic/Microsoft 로드맵은 agentic enterprise 방향 | Gartner 40% 취소, MIT NANDA 95% zero return, METR slowdown | 예측/비전과 실증 반례 | forecast와 evidence를 문장 강도로 구분 |

## 7. Critic / Repair / Expansion 상태

| 항목 | 상태 | 메모 |
| --- | --- | --- |
| Critic | 완료 | Research Adequacy Gate: Pass with constraints |
| Verifier | 완료 | `98-repair-notes.md`가 RQ-01~RQ-05를 지정 산출물 범위에서 대조 |
| Repair Queue | 완료 | 5개 항목 모두 supported. Journal에는 확신도/출처 유형/metric unit 보정 반영 |
| Expansion Queue | 보존 | 추가 리서치 라운드는 required no. 부족 증거는 최종 한계로 유지 |
| Journal Pass 2 | 완료 | Critic findings, Repair/Expansion Queue, Verifier correction, 최종 상충 상태, Synthesis notes 반영 |
| Negative Search | Researcher별 수행 기록 있음 | Journal은 검색하지 않았고, 각 산출물의 검색 로그만 구조화함 |

Critic findings 요약:

1. 최종 리포트는 "생산성 향상" 단정이 아니라 업무 조건별 효과와 비용이 갈리는 조건부 모델이어야 한다.
2. R1/R4의 실험·표준·보안 근거는 강하지만, R2/R3/R5의 고객 사례·제품 문서·로드맵은 문장 강도를 낮춰야 한다.
3. vendor-only 성과 수치는 출처 존재와 효과 크기 확신도를 분리해야 한다.
4. Codex/Claude Code 최신 기능과 모델 성능 발표는 capability/direction 근거이지 장기 ROI 실증이 아니다.
5. 보안 통제의 productivity tax는 ROI에 포함해야 하나 정량 공개 근거는 부족하다.
6. 비개발 업무 자동화는 자연어 대체가 아니라 업무의 소프트웨어화라는 귀납적 작동 가설로 표현해야 한다.

Repair Queue 상태:

| id | 상태 | Journal 반영 |
| --- | --- | --- |
| RQ-01 | supported / 완료 | Anthropic/Replit/Devin 수치를 `출처 존재`와 `효과 크기/ROI 확신도`로 분리 |
| RQ-02 | supported / 완료 | Codex use cases/workflow examples를 direct case가 아니라 official product recipe/documentation으로 보정 |
| RQ-03 | supported / 완료 | 제품 로드맵·모델 성능은 capability/direction 근거로 제한 |
| RQ-04 | supported / 완료 | MIT NANDA 95% zero return은 weak/report mirror 기반 반례 신호로 격하 |
| RQ-05 | supported / 완료 | Copilot, field RCT, 고객지원, BCG, METR, DORA 수치를 서로 다른 metric unit으로 유지 |

Expansion Queue 상태:

| id | 상태 | 최종 처리 |
| --- | --- | --- |
| EQ-01 | 보존 | 2026년형 Codex/Claude Code/Copilot의 동일 조직·동일 업무 net productivity는 증거 부족 |
| EQ-02 | 보존 | 일반 업무 자동화의 독립 성과와 실패율은 증거 부족 |
| EQ-03 | 보존 | guardrail productivity tax 정량값은 증거 부족 |
| EQ-04 | 보존 | agent-caused incident/near-miss 발생률과 손실 규모는 대표성 판단 불가 |
| EQ-05 | 보존 | Codex/Claude Code/Copilot/Devin/Replit head-to-head 비교는 도구 순위 결론 금지 |
| EQ-06 | 보존 | 업무의 소프트웨어화 프레임은 사례 귀납이며 독립 실증 부족 |

Verifier correction 요약:

| correction | 요약 |
| --- | --- |
| 확신도 분리 | official/vendor 수치는 원문 존재 확인과 효과 크기/ROI 확신도를 분리한다. |
| 출처 유형 보정 | Codex use cases는 고객 사례나 실험이 아니라 공식 제품 recipe/documentation이다. |
| ROI 과잉 해석 방지 | OpenAI/Anthropic/Microsoft/GitHub 로드맵은 방향성 근거이며 장기 순생산성 근거가 아니다. |
| 약한 출처 처리 | MIT NANDA 주장은 mirror/언론 재인용 기반의 경고 신호로만 유지한다. |
| metric unit 명시 | task completion time, completed tasks, RPH, human-rated quality, throughput/stability를 단일 생산성 수치로 혼합하지 않는다. |

최종 상충 상태:

| 상충 | Pass 2 상태 | Synthesis 처리 |
| --- | --- | --- |
| 단기 코딩 속도 개선 vs 실제 저장소 slowdown | 유지 | 과제 구조, 코드베이스 친숙도, 검증 비용의 조절 변수로 설명 |
| 개인 생산성 개선 vs delivery stability 악화 | 유지 | 개인/팀/운영 KPI를 분리 |
| vendor customer story 큰 배수 vs 독립 hands-on 실패 | 유지 | 가능성 신호와 ROI 확정 근거를 분리 |
| 자율 에이전트 로드맵 vs bounded autonomy 필요 | 유지 | 권한 tier, 승인, sandbox, audit log 중심으로 재정의 |
| 비개발 업무 자동화 vs 소프트웨어화 필요 | 유지 | 자연어 대체가 아니라 업무의 코드/API/검증 루프화로 표현 |
| 보안 통제의 위험 감소 vs 생산성 마찰 | 유지 | productivity tax는 정량 부족을 명시하고 ROI 비용 항목으로 포함 |
| 미래 낙관론 vs ROI 실패론 | 유지 | forecast/vendor survey와 실증/RCT/incident를 문장 강도로 구분 |

## 8. Synthesis 참고사항

최종 Synthesis는 "코딩 에이전트는 생산성을 올린다/못 올린다"의 단정이 아니라 업무 조건별 효과 모델로 구성하는 편이 산출물 근거와 맞다. 현재 근거는 다음 조건부 축으로 수렴한다.

| 축 | Synthesis에서 분리할 필요 |
| --- | --- |
| 과제 유형 | 짧고 명확한 greenfield, 반복 문서/테스트/QA, 고객지원, 컨설팅형 초안, mature repo 실제 이슈를 분리 |
| 지표 | task time, completed tasks, PR volume, review speed, delivery stability, escaped defects, support deflection, external spend를 분리 |
| 증거 품질 | peer-reviewed/official/direct case/vendor/community를 문장 강도로 구분 |
| 자동화 수준 | draft-only, PR-only, sandbox execute, network egress, production action의 권한 tier로 구분 |
| 조직 조건 | 테스트/리뷰/로그/rollback/API schema/runbook이 있는 조직과 암묵지·수동 SaaS UI 중심 조직을 구분 |
| 리스크 비용 | secure review, dependency review, secret scanning, incident response, compliance audit, prompt injection 방어 비용 포함 |
| 미래 방향 | long-horizon, computer use, multi-agent, agent identity, governance는 방향성 근거로 두되 장기 ROI와 분리 |

예비 Synthesis framing:

- "코딩 에이전트의 직접 가치는 코드 작성 속도보다 검증 가능한 업무 산출물의 생성-검토-배포 흐름을 재설계하는 데 있다."
- "성과가 큰 구간은 반복적이고 완료조건이 명확하며 rollback 가능하고 자동 검증이 있는 업무다."
- "성과가 약하거나 음수가 될 수 있는 구간은 고맥락·고위험·다파일·장기 유지보수·보안 민감·운영 side effect가 큰 업무다."
- "기업 도입은 모델 성능보다 권한, 데이터, 도구, 로그, 승인, 비용 한도의 설계 문제로 다뤄야 한다."
- "벤치마크와 vendor customer story는 가능성 근거이며, 구매/확대 결정은 내부 backlog 기반 PoC/RCT와 risk-adjusted KPI로 검증해야 한다."

Pass 2 Synthesis notes:

1. 중심 결론은 "코딩 에이전트는 조건부로 생산성을 높인다"이며, 조건은 명확한 완료조건, 검증 가능성, rollback 가능성, 낮은 권한 blast radius다.
2. 강한 근거는 짧고 명확한 코딩 과제, 반복 고객지원/지식업무, 일부 field experiment/RCT, 보안 실패 모드에 있다.
3. 약한 근거는 최신 Codex/Claude Code 자체 ROI, 일반 사무 산출물 자동화의 독립 성과, guardrail 비용, agent incident 발생률, 도구별 head-to-head 비교다.
4. 수치 인용은 출처 유형과 metric unit을 붙여야 하며, vendor/customer story의 큰 배수는 가능성 신호로만 사용한다.
5. 도입 권고는 agent identity, least privilege, sandbox, PR/draft-only, audit log, rollback, scanner, human approval을 포함한 risk-adjusted workflow 설계로 제시한다.
