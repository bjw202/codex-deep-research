# 공개 실제 사례와 정량 효과 - AI 자동화와 코딩급 에이전트 결합

**Researcher**: R1  
**Mode**: web  
**Date**: 2026-04-23  
**Scope**: n8n, Zapier/Make, Microsoft Power Automate/Copilot Studio, Workato/Claude, OpenAI Codex, GitHub Copilot 등 공개된 실제 기업/조직 사례와 정량 효과. 벤더 또는 고객사 발표만으로 확인되는 수치는 `vendor-only`로 표시했다. 최종 synthesis는 작성하지 않는다.

## 핵심 요약

- [Fact] 공개 사례는 “반복 데이터 이동 + AI 분류/요약/초안 + 사람 승인” 패턴에서 가장 강하다. Delivery Hero, Vodafone, Cineplex, Dunaway, Games Global, Stepstone, Musixmatch 등은 시간 절감, 비용 회피, 처리시간 단축을 수치로 공개했다.
- [Claim, vendor-only] n8n/Zapier/Make/Microsoft 고객사례의 대부분은 벤더가 발행한 사례다. 수치 자체는 구체적이지만 독립 감사 자료가 거의 없어, ROI 크기보다 “적용 업무 패턴”을 우선 근거로 써야 한다.
- [Fact] 코딩급 에이전트는 단순 자동완성보다 “PR 초안, 리팩터링, 테스트 생성, 코드 리뷰, 병렬 작업”에 초점이 옮겨가고 있다. GitHub-Accenture RCT는 PR 증가와 개발자 만족을 보고했고, OpenAI/Anthropic 고객사례는 초기 반복시간 단축과 영업/업무 준비 시간 단축을 제시한다.
- [Fact] 반례도 명확하다. METR의 2025년 RCT는 숙련 OSS 개발자가 익숙한 대규모 코드베이스에서 AI 도구 사용 시 19% 느려졌다고 보고했다. RPA/워크플로 자동화도 잘못 고른 프로세스, 취약한 거버넌스, 예외 처리 부재에서 실패율이 높다는 경고가 반복된다.
- [Claim] 실전 유즈케이스 후보는 “완전 자율”보다 “자동 수집/분류/초안화, 구조화된 실행, 사람이 검토할 증거 링크 제공”에 두면 성공 가능성이 높다.

## 읽는 법

이 문서는 최종 유즈케이스 도출을 위한 “실제 효과 근거 창고”다. 자동화 툴과 코딩급 에이전트를 결합할 때 어디서 시간이 줄고, 어디서 새 업무가 가능해지고, 어디서 위험이 생기는지 확인하는 데 쓰면 된다. 수치가 큰 사례일수록 벤더 발표인 경우가 많으므로, 그대로 ROI 예측에 넣기보다 유즈케이스 패턴과 측정 지표를 뽑는 용도로 읽어야 한다.

## 주요 발견

### 1. 반복 업무 자동화는 이미 정량 성과가 많다

가장 확실한 사례는 IT 계정 복구, 고객지원 환불, 문서 검색, 데이터 통합, 주문/인보이스 처리처럼 입력과 출력이 명확한 업무다. AI는 여기서 “판단 전체”를 맡기보다 분류, 요약, 정보 추출, 초안 생성을 담당하고, 워크플로 도구가 API 호출·티켓 생성·승인·로그를 담당한다.

| 상태 | 조직 | 도구 | 공개 시점 | 적용 업무 | 정량 효과 | 출처 성격 | 결론 영향 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [Claim, vendor-only] direct case | Vodafone UK | n8n Enterprise | 사례 페이지, 2025년 이후 추정. 워크플로는 2024-08 이후 | 사이버 보안 모니터링, SOAR, 피드 감시, 티켓 라우팅 | 33개 워크플로, 5,000+ person-days 절감, £2.2M 비용 회피, 2025년 월 약 £300k 지속 절감 | n8n 고객사례 | 보안 운영처럼 5분 단위 감시가 필요한 업무는 “사람이 하면 불가능한 주기”를 자동화할 수 있다. |
| [Claim, vendor-only] direct case | Delivery Hero | n8n Enterprise | 사례 페이지, 날짜 미표기 | 계정 잠금 복구: Okta/Jira/Google API, 관리자 승인 | 배포 5시간, 월 800건, 잠금 시간 35분→20분, 월 200시간 절감 | n8n 고객사례 | ITSM의 작은 병목도 대기업 규모에서는 월 수백 시간을 만든다. |
| [Claim, vendor-only] direct case | Stepstone | n8n self-hosted + AI parsing | 사례 페이지, 날짜 미표기 | 외부 채용 데이터 소스 통합, 광고 데이터 정제 | 통합 스프린트 2주→2시간, 25배 속도, 200+ 워크플로, 50개 내부 데이터 소스 | n8n 고객사례 | API 연결·데이터 변환은 코딩급 에이전트가 워크플로 생성/테스트를 돕기 좋은 영역이다. |
| [Claim, vendor-only] direct case | Musixmatch | n8n Enterprise | 사례 페이지, 날짜 미표기 | 클라이언트 데이터 요청, 내부 API 접근, 가사 문자 변환 | 4개월간 엔지니어링 47일 절감, 일부 요청 15초 처리, 27개 custom module | n8n 고객사례 | 비개발자가 내부 API를 안전하게 쓰게 만드는 “업무용 API 프런트”가 새 업무를 만든다. |
| [Claim, vendor-only] direct case | Field Aerospace | n8n self-hosted + AI | 사례 페이지, 날짜 미표기 | 정부 조달 공고 평가, 요구사항 매트릭스, 제안서 초안 | 제안서 80% 초안 2주/3-4명→25분, 요구사항 추출 수시간→15-20분, 연 $30k 소프트웨어 비용 제거 | n8n 고객사례 | “문서 긴 업무 + 승인된 내부 자료 + 사람 검토”는 AI 자동화의 강한 후보군이다. |
| [Claim, vendor-only] direct case | System AI / The Srama Group | n8n + WhatsApp/Twilio + AI + Zoho/Sheets | 사례 페이지, 날짜 미표기 | WhatsApp 음성/텍스트를 CRM·시트에 구조화 입력 | 작업 4-5분→10-20초, 90%+ 또는 97% 단축, 주 1일 절감, 부동산 온보딩→판매 62일→44일 | n8n 고객사례 | 채팅 인터페이스를 업무 실행 버튼으로 쓰는 패턴은 작은 팀의 운영 레버리지를 키운다. |
| [Claim, vendor-only] direct case | Dunaway | Microsoft Copilot Studio + Power Automate | 2025-12-11 | 규정 문서 수집·검색·질의응답 | 연 10,000시간 이상 쓰던 규정 검색 업무, 수동 조사 시간 90% 감소 | Microsoft 고객사례 | 규정·매뉴얼 RAG는 “근거 문서와 citation”이 붙을 때 실무성이 높다. |
| [Claim, vendor-only] direct case | Games Global | Microsoft Power Platform + Copilot Studio | 2025년 사례 | 부서별 자동화 워크숍, 규제 이메일, 고객지원, 계정 정리, 감사 보고 | 연 22,370시간 절감, 첫 워크숍 5,434시간, 고객지원 월 530시간, 재무 연 430시간 | Microsoft 고객사례 | 시민개발 + CoE 방식은 단일 대형 프로젝트보다 작은 자동화 포트폴리오로 성과를 낸다. |
| [Claim, vendor-only] direct case | Cineplex | Power Automate + Copilot Studio + generative AI | 2024년 전후 | 환불 처리, 이메일 문의 분류, 인보이스 세금 분류 | 환불 처리 5-15분→1분 미만, 보통 30초. 5개월 5,000건 처리. 이메일 문의 자동화는 연 1,300시간 예상 절감 | Microsoft 고객사례 | 고객지원은 “분류·정보 누락 감지·폼 요청·백엔드 실행”이 묶일 때 큰 효과가 난다. |
| [Claim, vendor-only] direct case | Zapier / Smith.ai | Zapier + ClickUp + custom JavaScript | 날짜 미표기 | 통화 전사 침묵 감지, 코칭 대상 통화 triage | 주 250+시간 절감, 코치가 실시간으로 문제 통화 확인 | Zapier 고객사례 | 사람이 전수검사하던 품질관리 업무를 자동 triage로 바꾸는 패턴이다. |
| [Claim, vendor-only] direct case | Zapier / Contractor Appointments | Zapier + OpenAI | 2025-05-07 | SMS 리드 응답, 예약, 장기 nurturing | Zapier 기반 lead flow로 $134M 고객 매출 귀속, 상단 퍼널 80-90% 자동 응답, 하루 20-50건 추가 예약, 연 $300k 증분 매출 | Zapier 블로그 고객사례 | “영업 응답 지연”은 자동화가 매출로 연결될 수 있는 대표 병목이다. 단, 귀속 매출은 독립 검증 필요. |
| [Claim, vendor-only] direct case | Zapier / SisterLove | Zapier + OpenAI | 날짜 미표기 | 키워드 기반 블로그·이메일·SMS·소셜 초안 | 9개월 24 business days, 192시간 절감. 일부 콘텐츠 organic keyword 1위 | Zapier 고객사례 | 1인 마케팅/비영리 팀에는 콘텐츠 변형·배포 자동화가 직접적인 시간 절감이다. |
| [Claim, vendor-only] direct case | Make / Greyt | Make + AI + Airtable/OpenAI | 2025년 전후 | 백오피스, 데이터 중복 검증, 내부 데이터 질의, 직원 온보딩 이미지 | 백오피스 비용 €125k 절감, 3 FTE 상당→0.5명, 프로젝트 수익성 2배 | Make 고객사례 | 데이터 정리와 내부 질의응답을 결합하면 “보고서 요청” 자체를 줄일 수 있다. |
| [Claim, vendor-only] direct case | Make / Dogsie | Make | 2022-08-12 | 구독 박스 주문 검토, 재고 확인, fulfillment 전달 | 주문 관리 시간 80%+ 절감, 500+ boxes/month, 같은 날 배송 가능 | Make 고객사례 | AI가 없어도 안정적 workflow 자동화가 핵심이며, AI는 예외·분류 계층에 붙이는 편이 안전하다. |

### 2. 코딩급 에이전트는 업무 자동화의 “제작·수리·검증” 레이어가 될 수 있다

Codex/Claude Code/ Copilot류는 최종 업무 실행 도구라기보다 자동화 시스템을 만드는 개발·검증 능력을 보강한다. 공개 사례에서는 API 연결, PR 작성, 테스트 생성, 코드 리뷰, 내부 시스템 질의용 MCP 서버, 다중 에이전트 병렬 작업이 반복적으로 나온다.

| 상태 | 조직 | 도구 | 공개 시점 | 적용 업무 | 정량 효과 | 출처 성격 | 결론 영향 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [Fact/Claim] direct case, partly stakeholder | Accenture + GitHub | GitHub Copilot | 2024-05-13 | 엔터프라이즈 개발 업무 RCT, telemetry와 설문 | PR/개발자 8.69% 증가, 제안 수락 약 30%, 90% 직무 만족 증가, 95% 코딩 즐거움 증가 | GitHub 연구 블로그, Accenture 협업 | 코딩 보조의 실제 효과는 PR, 빌드, 만족도 등 조직별 telemetry로 측정해야 한다. |
| [Claim, vendor-only] direct case | Harvey | OpenAI Codex | 2026년 현재 Codex 페이지 | 초기 반복 개발 | 초기 iteration time 30-50% 단축 | OpenAI 제품 페이지 고객 발언 | 자동화 생성·프로토타이핑 업무의 속도 가설을 뒷받침하지만 독립 검증은 없다. |
| [Claim, vendor-only] direct case | Sierra | OpenAI Codex | 2026년 현재 Codex 페이지 | 분기 단위 프로젝트, weekend shipping | “분기 걸리던 것을 주말에 ship”했다는 고객 발언 | OpenAI 제품 페이지 | “엄두 못 내던 프로젝트” 근거로 유용하지만 정량 검증은 낮다. |
| [Claim, vendor-only] direct case | Cisco Meraki | OpenAI Codex | 2026년 현재 Codex 페이지 | 다른 팀 코드베이스 refactor, test generation | 일정 유지, fully tested code 전달. 수치 없음 | OpenAI 제품 페이지 | 코드베이스 이동/릴리스 보조는 유즈케이스로 타당하나 효과 수치 부족. |
| [Claim, vendor-only] direct case | Workato | Claude + Claude Code + Workato Enterprise MCP | 2026년 현재 Claude 고객사례 | Claude를 사내 Gong/Salesforce/data systems와 연결, 영업 deal prep, 고객 성공 MCP | Claude 사용 700%+ 증가, 8개월 800+ MCP 서버, deal prep 3-4시간→45분, 30분 수동 시스템 확인→실시간 | Anthropic 고객사례 | 코딩급/에이전트 도구와 workflow platform의 결합은 “AI가 사내 시스템에 실제 액션을 취하는 연결층”에서 힘을 낸다. |

### 3. 새 업무 가능성은 “사람이 매번 못 하던 빈도·범위”에서 나온다

업무 단축보다 더 중요한 신호는 이전에는 비용 때문에 못 하던 일을 할 수 있게 된 사례다. Vodafone의 5분 단위 보안 피드 triage, Field Aerospace의 매일 조달 공고 평가, Contractor Appointments의 야간 SMS 예약, Dunaway의 수백 페이지 규정 즉시 검색이 여기에 해당한다.

| 가능해진 업무 | 사례 근거 | 왜 새 업무인가 | 유즈케이스 설계 힌트 |
| --- | --- | --- | --- |
| 5분 단위 보안 피드 감시와 triage | Vodafone/n8n | 사람이 24/7로 같은 빈도와 정확도로 확인하기 어렵다. | 알림만 보내지 말고 triage, 담당팀 티켓, 감사 로그까지 묶는다. |
| 매일 대량 조달 공고 평가 | Field Aerospace/n8n | 공고가 너무 많아 늦게 발견되던 기회를 앞당긴다. | scoring 기준과 내부 past performance 라이브러리를 분리해 검토 가능하게 한다. |
| 야간·비업무시간 리드 예약 | Contractor Appointments/Zapier+OpenAI | 사람이 대기하지 않아도 구매 의사가 높은 순간에 응답한다. | 자동 예약 전 검증 가능한 일정/지역/서비스 조건을 둔다. |
| 규정/매뉴얼 즉시 검색 | Dunaway/Copilot Studio+Power Automate | 엔지니어가 수백 페이지 문서를 가로질러 찾는 시간을 줄인다. | citation, jurisdiction 분리, 최신 문서 ingest 자동화가 핵심이다. |
| 비개발자 내부 API 접근 | Musixmatch/n8n, Stepstone/n8n | 개발자 티켓 없이 데이터 요청과 변환을 실행한다. | 권한·입력 검증·결과 링크를 workflow에서 강제한다. |

## 근거 표

이 표는 핵심 주장별로 출처의 강도와 직접성을 정리한다. `Fact`는 출처가 확인한 사실 또는 연구 설계가 공개된 주장, `Claim`은 이해관계자 발표에 의존하는 주장, `Unverified`는 단일 약한 출처나 독립 확인이 부족한 주장이다.

| 주장 | 근거 | 출처 유형 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| [Fact] 워크플로 자동화는 명확한 반복 업무에서 큰 시간 절감이 반복 보고된다. | Delivery Hero, Stepstone, Musixmatch, Microsoft Games Global/Cineplex/Dunaway, Zapier/Make 사례 다수 | official/primary, vendor-only 고객사례 | 출처 존재 높음, 효과 크기 중간 | https://n8n.io/case-studies/delivery-hero/ |
| [Claim] n8n은 ITSM, 보안, 데이터 통합, 제안서 초안에서 “코딩 없이/적은 코드로” 실무 처리 시간을 크게 줄였다. | n8n 고객사례 6건 이상, 모두 고객명·업무·수치 공개 | stakeholder/vendor-only | 중간 | https://n8n.io/case-studies/ |
| [Claim] Power Platform/Copilot Studio는 시민개발 포트폴리오 방식에서 연 수천~수만 시간 절감을 만들 수 있다. | Dunaway 90%, Games Global 22,370시간, Cineplex 30초 환불 처리 | official/vendor-only | 중간 | https://www.microsoft.com/en/customers/story/23332-games-global-microsoft-copilot-studio |
| [Fact/Claim] GitHub Copilot의 엔터프라이즈 효과는 조직 telemetry로 측정 가능하며 Accenture RCT에서는 PR 증가와 만족도 증가가 보고됐다. | GitHub-Accenture RCT: PR 8.69% 증가, 제안 수락 약 30%, 만족도 증가 | official/stakeholder 연구 | 중간-높음 | https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-in-the-enterprise-with-accenture/ |
| [Claim] Codex/Claude Code류는 자동화 제작, 코드 리뷰, refactor, 테스트 생성, MCP 연결 업무에 쓰이고 있다. | OpenAI Codex 고객 발언, Anthropic Workato 고객사례 | vendor-only | 중간 | https://openai.com/codex/ |
| [Fact] 숙련 개발자에게 AI 코딩 도구가 항상 빠른 것은 아니다. | METR 2025 RCT: 익숙한 OSS 코드베이스 작업에서 AI 사용군 19% 느림 | independent/primary research | 높음 | https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/ |
| [Fact] 자동화/RPA 실패는 프로세스 선택, governance, 예외 처리, 유지보수에서 반복된다. | EY 30-50% 초기 RPA 실패 추정이 여러 분석에서 재인용, RPA 한계 연구 다수 | independent analysis + stakeholder | 중간 | https://www.allata.com/insights/avoiding-rpa-implementation-mistakes-and-failures/ |
| [Fact] 저코드 자동화의 성능 개선은 실험에서도 보인다. | n8n 소규모 실험: 평균 185.35초 수동→1.23초 자동, 5% 오류→0 관찰 오류 | academic/preprint | 중간 | https://arxiv.org/abs/2602.01311 |
| [Fact] 생성형 AI+IDP+RPA는 영수증/비용 처리 같은 문서 업무에서 큰 단축 가능성이 있다. | 한국 대기업 Company S 사례: 종이 영수증 경비 처리 시간 80%+ 감소 | academic/preprint | 중간 | https://arxiv.org/abs/2505.20733 |

## 출처 품질 매트릭스

공개 사례는 풍부하지만 독립 감사는 부족하다. 따라서 이 관점의 결론은 “어떤 업무 패턴이 반복적으로 효과를 냈는가”에는 비교적 강하고, “각 벤더가 주장한 ROI 수치를 그대로 믿어도 되는가”에는 약하다.

| 출처 유형 | 개수 | 핵심 기여 | 약점 |
| --- | ---: | --- | --- |
| official / primary | 14 | n8n, Microsoft, Zapier, Make, GitHub, OpenAI, Anthropic 고객사례와 연구 발표 | 대부분 벤더 이해관계가 있어 효과 수치의 독립 검증 부족 |
| academic / standard / patent | 4 | n8n 소규모 실험, Company S 경비 처리, METR 코딩 RCT, AI coding maintenance burden 연구 | 일부 preprint이며, enterprise 운영 사례와 조건이 다를 수 있음 |
| direct case / experiment | 16+ | 조직명·업무·효과 수치가 있는 사례 확보 | 측정 방식이 사례마다 달라 직접 비교 부적절 |
| vendor / stakeholder | 14 | 실무 적용 업무와 수치가 구체적 | 마케팅 편향, 실패 사례 미공개 가능성 |
| reliable independent / analysis | 4 | METR 보도/분석, Stanford AI Index, InfoWorld/ITPro/Time류 보도, RPA 실패 분석 | 일부는 원 연구 재인용이며 직접 현장 감사는 아님 |
| community | 5+ 검색 확인 | 자동화 유지보수, 비용, 실패감, tool fit 문제 확인 | 익명·개별 경험이라 일반화 불가 |
| weak / unverified | 다수 검색 결과 배제 | 소규모 agency/블로그의 시간 절감 주장 | 고객명 불명, 수치 검증 불가 |

## 반례/실패 사례 검색 로그

실패 검색의 결론은 단순하다. “AI 자동화가 시간을 줄인다”는 주장은 업무가 작고 반복적이며 검증 가능한 경우에 강하고, 장기 맥락·복잡한 코드베이스·예외가 많은 프로세스에서는 유지보수와 검증 비용이 절감분을 상쇄할 수 있다.

| 쿼리 | 목적 | 결과 | 결론 영향 |
| --- | --- | --- | --- |
| `AI coding agents productivity slower experienced developers METR 2025 study 19%` | 코딩 에이전트/AI 코딩 반례 확인 | METR RCT와 다수 독립 보도 확인. 익숙한 대형 OSS 코드베이스에서 16명, 246개 실제 task, AI 사용 시 19% 느림. | 코딩 에이전트는 “모든 개발 업무 단축”이 아니라 task selection과 검증 설계가 필요하다. |
| `RPA failure rate enterprise automation projects research 30 50 percent failure` | RPA/자동화 실패율 확인 | EY 30-50% 초기 RPA 실패 추정이 여러 분석에서 반복 인용. 원자료 접근성은 제한적. | workflow 자동화도 process mining, governance, 예외 처리가 없으면 실패한다. |
| `workflow automation risk AI agent failure hallucination enterprise 2025 report` | AI agent가 workflow를 오작동시키는 위험 확인 | hallucination, 권한 오남용, agent observability 부족, Zap/n8n history 한계에 대한 분석·커뮤니티 사례 확인. | 고객 대응·결제·권한 작업은 human approval과 audit log가 필수다. |
| `automation failure AI agents caused incident case study coding agent limitations` | 실제 사고/한계 사례 탐색 | 공개 대형 사고 사례는 제한적. 대신 Copilot PR tip/광고 삽입 논란, agent output cleanup 부담, 보안/권한 우려가 확인됨. | “실패 공개가 적다” 자체가 불확실성이다. 내부 pilot에서 실패 로그를 수집해야 한다. |
| `n8n automation failure regret workflow broke production Reddit` | n8n/Zapier/Make 유지보수 실패감 탐색 | 6주 자동화가 오히려 시간 낭비였다는 경험, 담당자 이탈 후 자동화 붕괴, agent hallucination 추적 어려움 등 커뮤니티 글 확인. | no-code 자동화도 문서화와 ownership이 없으면 기술부채가 된다. |
| `Power Automate AI Builder limitation throttling invoice processing` | Power Automate 확장 한계 탐색 | Concentrix 사례에서 대량 invoice 20,000/month 접근 시 모델 유지관리와 throttling limit 언급. | 대량 문서 처리에서는 플랫폼 한도와 모델 유지관리 비용을 설계 초기에 반영해야 한다. |

## 상충점과 불확실성

- 벤더 고객사례는 효과 수치가 구체적이지만, 실패한 pilot이나 유지보수 비용을 거의 공개하지 않는다. 따라서 “성공 패턴” 근거로는 유효하지만 “평균 ROI” 근거로 쓰면 과장될 수 있다.
- GitHub Copilot/Accenture 계열 연구는 긍정적이고 METR 연구는 부정적이다. 상충은 모순이라기보다 조건 차이다. Accenture는 enterprise adoption과 DevOps telemetry, METR은 숙련 OSS 개발자가 이미 잘 아는 코드베이스에서 실제 issue를 푸는 조건이다.
- Codex/Claude Code 고객 발언은 현재 가장 최신 실무 신호지만 대부분 정량 방법론이 없다. “초기 반복 30-50% 단축” 같은 수치는 강한 아이디어 근거이나, 최종 실행안에서는 내부 benchmark가 필요하다.
- n8n과 Zapier/Make/Microsoft 사례는 자동화 도구가 중심이고, Codex/Claude Code가 직접 결합된 공개 사례는 상대적으로 적다. 결합 유즈케이스는 사례를 그대로 복사하기보다 “업무 workflow + agent가 생성/수리/검증” 구조로 추론해야 한다.

## 의사결정 영향

바로 실행 후보로 볼 수 있는 업무는 네 조건을 만족한다. 입력이 이미 디지털이고, 성공/실패 판정 기준이 있으며, API나 RPA로 실행할 수 있고, 사람이 검토해야 할 evidence를 남길 수 있어야 한다. 이 조건에서는 n8n/Zapier/Make/Power Automate가 실행 레이어, Codex/Claude Code가 workflow 코드·API glue·테스트·문서화·운영 점검 레이어가 된다.

반대로 고객에게 직접 발송되는 문장, 결제·권한·보안 변경, 법무/규정 해석, 핵심 코드 변경은 완전 자동 실행보다 “초안 + 검증 + 승인”으로 시작해야 한다. METR와 RPA 실패 근거를 반영하면, 절감 시간을 계산할 때는 생성 시간뿐 아니라 검토·수정·장애 대응·ownership 비용을 포함해야 한다.

## 인접 질문

- 최종 유즈케이스 10개를 만들 때 “업무 실행 자동화”와 “자동화 제작/수리 자동화”를 분리할 것인가? 이 둘의 KPI가 다르다.
- 대상 독자가 1인/소규모 팀인지, 엔터프라이즈 운영팀인지에 따라 tool choice가 달라진다. n8n self-hosting, Zapier managed simplicity, Microsoft tenant integration, Workato governance의 우선순위를 먼저 정해야 한다.

## 출처 목록

| # | 출처 | 날짜/버전 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| 1 | n8n Vodafone case study | 페이지 날짜 미표기, 2024-08 이후 워크플로 언급 | 중간 | https://n8n.io/case-studies/vodafone/ |
| 2 | n8n Delivery Hero case study | 페이지 날짜 미표기 | 중간 | https://n8n.io/case-studies/delivery-hero/ |
| 3 | n8n Stepstone case study | 페이지 날짜 미표기 | 중간 | https://n8n.io/case-studies/stepstone/ |
| 4 | n8n Musixmatch case study | 페이지 날짜 미표기 | 중간 | https://n8n.io/case-studies/musixmatch/ |
| 5 | n8n Field Aerospace case study | 페이지 날짜 미표기 | 중간 | https://n8n.io/case-studies/field-aerospace/ |
| 6 | n8n System AI case study | 페이지 날짜 미표기 | 중간 | https://n8n.io/case-studies/system-ai/ |
| 7 | Microsoft Dunaway customer story | 2025-12-11 | 중간 | https://www.microsoft.com/en/customers/story/25879-dunaway-microsoft-copilot-studio |
| 8 | Microsoft Games Global customer story | 2025년 전후 | 중간 | https://www.microsoft.com/en/customers/story/23332-games-global-microsoft-copilot-studio |
| 9 | Microsoft Cineplex customer story | 2024년 전후 | 중간 | https://www.microsoft.com/en/customers/story/1751257654493783966-cineplex-telecommunications-power-automate-en-canada |
| 10 | Zapier Smith.ai customer story | 날짜 미표기 | 중간 | https://zapier.com/es/customer-stories/smith-ai |
| 11 | Zapier Contractor Appointments customer story | 2025-05-07 | 중간 | https://zapier.com/blog/contractor-appointments-books-millions-with-ai-automation/ |
| 12 | Zapier SisterLove customer story | 날짜 미표기 | 중간 | https://zapier.com/customer-stories/sisterlove |
| 13 | Make Greyt success story | 2025년 전후 | 중간 | https://www.make.com/en/success-stories/how-make-helped-greyt-save-back-office-costs |
| 14 | Make Dogsie success story | 2022-08-12 | 중간 | https://www.make.com/en/success-stories/automate-order-management-case-study |
| 15 | GitHub/Accenture Copilot RCT blog | 2024-05-13 | 중간-높음 | https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-in-the-enterprise-with-accenture/ |
| 16 | OpenAI Codex product/customer page | 2026-04 확인 | 중간 | https://openai.com/codex/ |
| 17 | Anthropic Claude customer story: Workato | 2026-04 확인 | 중간 | https://claude.com/customers/workato |
| 18 | METR, Early-2025 AI and experienced OSS developer productivity | 2025-07-10 | 높음 | https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/ |
| 19 | arXiv: Evaluating Workflow Automation Efficiency Using n8n | 2026-02-01 | 중간 | https://arxiv.org/abs/2602.01311 |
| 20 | arXiv: E2E Process Automation Leveraging Generative AI and IDP-Based Automation Agent | 2025-05 | 중간 | https://arxiv.org/abs/2505.20733 |
| 21 | arXiv: AI-assisted Programming May Decrease Productivity... | 2025-10 | 중간 | https://arxiv.org/abs/2510.10165 |
| 22 | Stanford HAI AI Index 2026 Chapter 4 Economy | 2026 | 중간 | https://hai.stanford.edu/assets/files/ai_index_report_2026_chapter_4_economy.pdf |
| 23 | Allata, Avoiding RPA implementation mistakes and failures | 2023 전후 | 중간 | https://www.allata.com/insights/avoiding-rpa-implementation-mistakes-and-failures/ |
| 24 | InfoWorld, AI coding tools can slow down seasoned developers | 2025 | 중간 | https://www.infoworld.com/article/4020931/ai-coding-tools-can-slow-down-seasoned-developers-by-19.html |

## 검색 포화 판단

공식/1차 출처는 요구 기준 3개를 크게 넘겼고, 독립 보도/분석도 METR 관련 보도, Stanford AI Index, RPA 실패 분석 등으로 2개 이상 확보했다. 직접 사례는 정량 수치가 있는 것만 10개 이상 찾았으며, n8n·Zapier·Make·Microsoft·GitHub/OpenAI/Anthropic 계열을 모두 포함했다.

더 검색해도 새로 늘어날 가능성이 낮은 것은 “벤더 고객사례의 변형”이다. 반대로 아직 부족한 것은 Codex/Claude Code가 n8n/Zapier/Power Automate workflow를 직접 생성·운영한 독립 사례, 그리고 벤더 발표 ROI를 외부 감사한 자료다. 다음 라운드가 있다면 실제 사용 기업 인터뷰, GitHub PR telemetry, 내부 자동화 실패 로그처럼 원자료에 가까운 데이터를 찾아야 한다.
