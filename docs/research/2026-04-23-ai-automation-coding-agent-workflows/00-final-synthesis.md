# 최종 리포트 - Codex와 Claude Code로 만드는 업무 자동화 혁신안

**Date**: 2026-04-23  
**Workspace**: `docs/research/2026-04-23-ai-automation-coding-agent-workflows/`

## 한 줄 결론

Codex와 Claude Code는 단순한 코딩 도구가 아니라, 반복 업무를 "검토 가능한 산출물"로 바꾸는 업무 엔진으로 써야 한다. n8n 같은 자동화 도구는 일을 연결하고, Codex와 Claude Code는 초안, 코드, 검증 자료, 승인 패킷을 만들며, 사람은 마지막 결정을 승인한다.

## 3분 요약

이번 리서치의 핵심은 단순하다. AI에게 업무를 통째로 맡기면 위험하다. 대신 업무를 작은 흐름으로 쪼개고, AI가 사람이 검토할 수 있는 결과물을 만들게 하면 강력해진다.

가장 좋은 시작점은 세 부류다. 첫째, 개발/IT처럼 코드, 테스트, 리뷰 체계가 이미 있는 업무다. 둘째, 구매, 법무, 재무처럼 문서와 판단 근거를 모으는 데 시간이 오래 걸리는 업무다. 셋째, 보안, 품질, 설비 유지보수처럼 사람이 계속 감시하기 어렵지만 잘못 실행하면 위험한 업무다.

n8n, Zapier, Make, Power Automate 같은 도구는 이메일, Slack, Jira, ERP, Google Drive, GitHub 같은 시스템을 이어준다. Codex와 Claude Code는 그 위에서 코드를 고치고, 문서를 읽고, 표를 만들고, 테스트를 돌리고, 보고서 초안을 만든다. 중요한 것은 AI가 바로 보내고, 결제하고, 배포하고, 계약을 확정하지 않게 하는 것이다.

따라서 첫 90일은 "자동 실행"이 아니라 "자동 준비"에 집중해야 한다. AI가 PR, 계약 redline, supplier risk packet, 월마감 exception list, work order 초안을 만들고 사람이 승인하는 방식으로 시작한다.

## 핵심 답변

사용자가 원하는 방향은 충분히 가능하다. 다만 표현을 정확히 해야 한다. 목표는 "AI 직원에게 일을 전부 맡기는 것"이 아니다. 목표는 반복 업무를 코드처럼 다룰 수 있게 만드는 것이다.

예를 들어 구매팀의 supplier onboarding을 보자. 지금은 담당자가 이메일을 뒤지고, 사업자등록증과 계좌 정보를 확인하고, ERP에 중복 공급사가 있는지 찾고, 누락 서류를 다시 요청한다. 자동화 후에는 n8n이 supplier portal, ERP, 제재 목록 API, AP 시스템을 연결한다. Codex나 Claude Code는 중복 공급사 탐지 로직, 누락 서류 목록, 위험 메모, 승인 체크리스트를 만든다. 최종 등록과 계좌 변경은 구매, AP, 리스크 담당자가 승인한다.

이런 방식이면 AI는 일을 "결정"하지 않는다. AI는 사람이 더 빨리 결정할 수 있게 자료를 준비한다. 이것이 현재 공개 근거와 보안 조건을 모두 만족하는 가장 현실적인 혁신안이다.

## 무엇이 달라지는가

기존 자동화는 대개 "A 시스템에서 B 시스템으로 데이터를 옮긴다"에 머물렀다. 이번 방식은 한 단계 더 간다. 에이전트가 업무 맥락을 읽고, 필요한 파일과 데이터를 모으고, 검토 가능한 산출물을 만든다.

개발자는 작은 버그 수정, 테스트 보강, 문서 업데이트를 직접 처음부터 하지 않아도 된다. 에이전트가 이슈를 읽고 PR을 만들며, CI가 통과했는지 확인한다. 개발자는 diff와 테스트 결과를 보고 승인한다.

법무팀은 계약서를 처음부터 훑기보다, 표준 조항과 다른 부분, 협상 쟁점, 위험 조항이 정리된 redline 초안을 먼저 본다. 변호사는 최종 법률 판단에 집중한다.

구매팀은 공급사 제안서를 엑셀에 다시 옮기지 않는다. 에이전트가 요구사항 충족도, 가격 비교, 리스크, 누락 질문을 정리한다. 소싱 위원회는 평가표와 근거를 보고 판단한다.

재무팀은 월마감 때 숫자를 복사하고 설명 문구를 반복 작성하는 시간을 줄인다. 에이전트가 ERP와 보조원장을 대조하고, 차이가 큰 항목과 근거 거래를 묶어준다. 회계 owner는 예외와 설명을 검토한다.

## 무엇을 하면 좋은가

먼저 5개 파일럿으로 시작하는 것이 좋다.

1. **개발/IT: Issue-to-PR 자동화**  
   Jira나 GitHub 이슈가 들어오면 Codex 또는 Claude Code가 branch를 만들고, 작은 수정과 테스트를 포함한 PR을 만든다.

2. **보안/운영: Alert triage와 remediation packet**  
   보안 알림이나 장애 알림이 들어오면 로그를 요약하고, 원인 후보와 대응 체크리스트, 설정 변경 PR 초안을 만든다.

3. **구매: Supplier onboarding 검증 패킷**  
   신규 공급사 서류, 계좌, 세금 정보, 제재 목록, ERP 중복 여부를 확인해 승인 패킷을 만든다.

4. **법무: 계약 redline과 협상 이슈표**  
   계약서가 들어오면 표준 조항과 다른 부분, 위험 조항, fallback position을 정리한다.

5. **재무: 월마감 variance/reconciliation pack**  
   ERP, 보조원장, 스프레드시트를 대조해 차이 항목, 원인 후보, 설명 초안을 만든다.

이 5개는 공통점이 있다. 산출물이 남고, 검증할 수 있고, 승인자가 분명하다. 그래서 처음부터 무리한 전사 자동화보다 성공 가능성이 높다.

## 우선순위 제안

아래 표는 "검증된 ROI 순위"가 아니다. 공개 사례, 구현 가능성, 위험 통제 가능성, Codex/Claude Code 적합성을 함께 본 파일럿 우선순위다.

| 우선 | 업무 | 무엇을 자동 준비하나 | 사람은 무엇을 승인하나 | 첫 PoC |
| ---: | --- | --- | --- | --- |
| 1 | Issue-to-PR | 코드 변경, 테스트, PR 설명 | PR merge | 한 repo에서 작은 버그/문서/테스트 티켓 20개 |
| 2 | CI 실패 분석 | 실패 원인, 수정 PR, runbook 초안 | 수정 PR, 배포 여부 | 실패한 GitHub Actions 로그 자동 분석 |
| 3 | 보안 alert triage | 심각도, 관련 로그, 조치 초안 | 보안 조치, change window | SIEM/Jira/Slack 연결 |
| 4 | Supplier onboarding | 서류 검증, 중복 탐지, 위험 패킷 | 공급사 등록, 계좌 변경 | 신규 공급사 30건 |
| 5 | 계약 redline | 표준 조항 이탈, 위험 조항, 협상표 | 법무 의견, 계약 승인 | NDA/MSA 20건 |
| 6 | 월마감 대조 | 차이 항목, 근거 거래, 설명 초안 | 회계 판단, 조정 입력 | 3개 계정 reconciliation |
| 7 | AP/Expense exception | 누락 영수증, 정책 위반, 지급 보류 추천 | 지급/보류 결정 | 비용 예외 큐 100건 |
| 8 | 설비 work order | 고장 증상, 과거 이력, 부품, 안전 체크 | 현장 작업 지시 | CMMS 이력 기반 초안 |
| 9 | 품질 CAPA packet | 불량 lot 추적, 원인 후보, 조치 초안 | CAPA 승인 | NCR 10건 |
| 10 | 경영회의 보고 패키지 | KPI, 재무, 리스크, action owner 대조 | 보고서 배포 | 월간 회의 deck 1회 |
| 11 | 정책/SOP 변경 영향 | 영향받는 문서, 체크리스트, 교육 항목 | 프로세스 변경 | SOP 3건 |
| 12 | 온보딩/오프보딩 감사 | 권한 누락, 과다 권한, 미완료 task | 권한 부여/회수 | 입퇴사 20건 |
| 13 | RFP/RFQ 평가 | 제안서 정규화, TCO 비교, award memo | 공급사 선정 | RFQ 1건 |
| 14 | 반복 보고서 refresh | SQL, 차트, 이상치, row count 검증 | 보고서 게시 | 주간 리포트 4회 |
| 15 | 규제 변경 영향 | 법령 변경과 내부 control 매핑 | 대응 과제 승인 | 규제 알림 5건 |

## 핵심 사례

### 1. 개발/IT: 이슈가 PR까지 가는 시간 줄이기

현재 개발자는 작은 티켓에도 저장소를 찾고, 관련 코드를 읽고, 테스트를 만들고, PR 설명을 써야 한다. 이 작업은 중요하지만 반복적이다. Codex나 Claude Code가 이슈를 읽고, 관련 파일을 찾고, 작은 수정과 테스트를 포함한 PR을 만든다. GitHub Actions가 테스트를 돌리고, 개발자는 diff와 테스트 결과를 보고 merge 여부를 정한다. 이 방식은 코딩 에이전트의 공개 사용처와 가장 직접적으로 맞는다.

첫 PoC는 작게 잡아야 한다. 한 저장소에서 문서 수정, 테스트 보강, 작은 버그 수정처럼 실패해도 되돌리기 쉬운 티켓 20개를 고른다. 성공 기준은 "AI가 만든 PR 수"가 아니다. merge된 PR 비율, 리뷰 시간, 재작업률, 테스트 실패율을 본다.

### 2. 구매: supplier onboarding을 승인 패킷으로 바꾸기

구매팀의 병목은 대개 판단 자체보다 자료 수집이다. 서류가 빠졌는지, 중복 공급사가 있는지, 계좌가 바뀌었는지, 제재 목록에 걸리는지 확인하는 데 시간이 든다. n8n은 supplier portal, ERP, AP, 외부 검증 API를 연결한다. Codex나 Claude Code는 누락 서류 목록, 중복 후보, 위험 사유, 승인 체크리스트를 만든다.

이 업무에서 AI가 공급사를 승인하면 안 된다. AI는 패킷을 만들고, 구매/AP/법무/리스크 담당자가 승인한다. 특히 bank account change는 2인 승인으로 둬야 한다. 첫 PoC는 신규 공급사 30건을 대상으로 cycle time, 누락 서류율, 승인 반려율을 측정하면 된다.

### 3. 법무: 계약 검토를 redline 초안으로 시작하기

법무팀은 계약서마다 표준 조항과 다른 부분을 찾고, 과거 협상 입장을 확인하고, business owner에게 쟁점을 설명한다. Claude Code나 Codex는 clause library와 playbook을 읽고, 계약서의 이탈 조항을 표시하고, 협상 이슈표를 만든다. n8n은 CLM, 이메일, CRM, 구매 시스템에서 계약 요청을 받아 검토 큐를 만든다.

여기서도 AI는 법률 의견의 최종 작성자가 아니다. 법률 분야에서는 가짜 판례와 잘못된 인용 사례가 반복적으로 보고됐다. 따라서 계약 redline, 법률 리서치, 규제 영향 분석은 모두 변호사 승인 전까지 초안으로만 남겨야 한다.

### 4. 재무: 월마감 자료를 자동으로 대조하기

월마감은 숫자를 복사하는 일이 아니라 숫자가 왜 다른지 설명하는 일이다. 에이전트는 ERP, 보조원장, 스프레드시트, BI 데이터를 읽고 계정별 차이를 찾는다. 큰 차이가 있는 항목은 근거 거래와 함께 묶고, 설명 초안을 만든다. n8n은 close calendar에 맞춰 데이터를 가져오고, 담당자 승인 요청을 보낸다.

사람은 회계 판단을 유지한다. 에이전트가 만든 reconciliation workbook과 exception list를 보고 account owner와 controller가 승인한다. 첫 PoC는 3개 계정만 대상으로 잡고, 마감 소요 시간과 감사 질의 감소 여부를 본다.

### 5. 산업운영/품질: 현장 지식을 work order와 CAPA로 만들기

설비 유지보수와 품질 문제는 데이터가 많아도 사람이 한 번에 보기 어렵다. 정비 이력, 매뉴얼, 센서 로그, 작업자 메모, 품질 검사 결과가 흩어져 있다. 에이전트가 이 자료를 묶어 원인 후보, 필요한 부품, 안전 체크리스트, work order 초안을 만든다. 품질 문제라면 불량 lot, 공정 조건, 유사 CAPA를 찾아 원인 분석 초안을 만든다.

이 영역은 물리 안전과 직결된다. AI가 설비를 직접 제어하거나 현장 조치를 자동 확정하면 안 된다. 첫 단계는 현장 supervisor와 안전 담당자가 볼 수 있는 troubleshooting packet 또는 CAPA packet을 만드는 것이다.

## 실행 로드맵

### 0-30일: 자동 실행이 아니라 자동 준비부터 시작

첫 달에는 권한을 낮게 잡는다. 에이전트가 읽고, 분석하고, branch나 문서 초안을 만들 수는 있어도 고객 발송, 결제, 권한 변경, production 배포는 하지 못하게 한다.

해야 할 일은 네 가지다. 첫째, 파일럿 3-5개를 고른다. 둘째, 각 업무의 owner와 승인자를 정한다. 셋째, 현재 baseline을 잰다. 넷째, 모든 실행 기록을 남길 run log를 만든다.

### 31-60일: 반복 운영하면서 실패를 모은다

두 번째 달에는 잘 된 사례보다 실패 사례를 더 중요하게 본다. 에이전트가 틀린 자료를 읽었는지, 승인자가 너무 오래 걸리는지, 자동 검증이 충분한지 확인한다. 보안 관점에서는 외부 문서, Slack 메시지, 이슈 본문 안에 숨은 지시가 들어와도 에이전트가 위험한 행동을 하지 않는지 테스트한다.

이 시점의 목표는 확장이 아니다. "어디서 멈춰야 하는지"를 배우는 것이다.

### 61-90일: 확장할지, 줄일지 결정

세 번째 달에는 증거를 보고 판단한다. cycle time이 줄었는지, 리뷰 시간이 늘지는 않았는지, 재작업이 많아졌는지, 보안 경고가 늘었는지 본다. 순효과가 좋으면 팀을 1-2개 더 늘린다. 효과가 애매하면 업무 범위를 더 작게 자른다.

90일 안에는 production direct action을 열지 않는 편이 안전하다. 배포, 결제, HR 변경, 법무 최종 의견, 보안 정책 변경은 별도 승인 체계가 준비된 뒤에만 논의한다.

## 좋은 워크플로우의 모양

좋은 자동화는 복잡해 보이지 않는다. 아래 흐름을 반복한다.

```text
업무가 들어온다
-> 필요한 자료를 모은다
-> 위험도에 따라 경로를 나눈다
-> 에이전트가 초안/PR/패킷을 만든다
-> 테스트나 대조 검사를 한다
-> 사람이 승인한다
-> 승인된 것만 실행한다
-> 실행 기록을 남긴다
```

이 구조에서 n8n은 업무가 들어오고 나가는 길을 만든다. Codex와 Claude Code는 중간 산출물을 만든다. GitHub Actions, 스키마 검증, 보안 스캐너, reconciliation script는 자동 검증을 맡는다. 사람은 마지막 판단을 한다.

## 도입 원칙

| 원칙 | 쉬운 설명 | 적용 예 |
| --- | --- | --- |
| 바로 실행하지 않는다 | AI는 먼저 초안을 만든다 | 계약 redline, PR, risk packet |
| 사람이 볼 수 있게 남긴다 | 결과물과 근거가 있어야 한다 | diff, 테스트 로그, source link |
| 작은 업무부터 시작한다 | 실패해도 되돌릴 수 있어야 한다 | 문서 수정, 테스트 보강, 예외 큐 정리 |
| 권한을 나눈다 | 읽기, 초안, 수정, 실행을 분리한다 | branch write는 허용, production write는 금지 |
| 성과는 순효과로 본다 | 검토와 재작업 비용을 뺀다 | cycle time - review/rework cost |
| 업무 owner를 둔다 | 자동화도 담당자가 있어야 한다 | process owner, approver, risk owner |

## 주요 근거

공개 사례는 "반복 업무 + 분류/요약/초안 + 승인" 패턴에서 가장 강하다. n8n 고객사례에는 Delivery Hero의 계정 잠금 복구, Vodafone의 보안 workflow, Field Aerospace의 조달 공고 평가가 있다. Microsoft 사례에는 Dunaway의 규정 검색, Games Global의 시민개발 자동화, Cineplex의 환불 처리가 있다. Zapier와 Make 사례도 리드 응답, 콘텐츠 변형, 주문 처리, 백오피스 자동화에서 시간을 줄였다고 보고한다.

다만 이 수치들은 대부분 벤더나 고객사가 직접 발표한 사례다. 그래서 "이런 업무가 자동화 후보가 된다"는 근거로는 쓸 수 있지만, "우리 회사도 같은 비율로 절감된다"는 근거로 쓰면 안 된다.

프런티어 AI 회사들의 방향도 일치한다. OpenAI, Anthropic, Google은 모두 2025-2026년에 단순 채팅 보조에서 파일, 터미널, 브라우저, 업무 앱을 다루는 에이전트로 이동했다. 동시에 세 회사 모두 권한, 샌드박스, 승인, 로그, 네트워크 제한을 강조한다. 즉 제품 방향은 더 강한 에이전트지만, 운영 방식은 더 분명한 통제다.

## 주의할 점과 실패 조건

첫째, AI가 항상 빠른 것은 아니다. METR의 2025년 연구는 숙련 개발자가 익숙한 오픈소스 코드베이스에서 AI 도구를 썼을 때 오히려 19% 느려졌다고 보고했다. 이 결과는 모든 AI 코딩 도구가 나쁘다는 뜻이 아니다. 익숙한 복잡한 업무에서는 검토, 대기, 수정 비용이 절감분을 넘을 수 있다는 뜻이다.

둘째, 법무와 구매는 특히 보수적으로 접근해야 한다. 법무에서는 AI가 만든 가짜 판례와 잘못된 인용 문제가 실제 제재 사례로 이어졌다. 구매에서는 supplier master data 품질, 중복 공급사, 계좌 변경 fraud가 큰 위험이다. 이 영역은 자동 판단이 아니라 승인 패킷 생성으로 제한해야 한다.

셋째, 외부 도구 연결은 편리하지만 위험도 키운다. MCP 같은 도구 연결 표준, 브라우저 조작, Slack/Notion 문서 읽기는 업무 범위를 넓힌다. 동시에 문서나 메시지 안의 악성 지시가 에이전트를 속일 수 있다. 그래서 외부 내용을 읽는 에이전트에게는 쓰기 권한과 외부 전송 권한을 좁게 줘야 한다.

넷째, ROI를 사용량으로 판단하면 실패한다. "에이전트 호출 수", "생성된 PR 수", "작성된 문서 수"는 성공 지표가 아니다. 실제로 줄어든 시간, 승인 반려율, 재작업, 품질 문제, 보안 경고, 운영 비용까지 봐야 한다.

## 무엇을 자동화하지 말아야 하는가

처음 90일에는 아래 업무를 자동 실행하지 않는 것이 좋다.

- 고객에게 직접 보내는 이메일이나 계약 문구
- 결제, 환불, 계좌 변경, vendor master 변경
- production 배포, DB migration, 보안 정책 변경
- HR 권한 부여, 해고/평가/보상 관련 판단
- 법률 의견, 규제 해석, 소송 전략
- 설비 제어, 안전 절차 변경, 현장 작업 확정

이 업무들은 AI가 초안과 근거를 만들 수는 있다. 하지만 최종 실행은 사람이 승인해야 한다.

## 상충점과 판단

| 상충점 | 한쪽 근거 | 다른 쪽 근거 | 판단 |
| --- | --- | --- | --- |
| AI 자동화는 시간을 줄이는가 | 여러 벤더 고객사례가 큰 절감을 보고한다 | 실패한 PoC와 유지보수 비용은 공개가 적다 | 가능성은 크지만 내부 baseline으로 검증해야 한다 |
| 코딩 에이전트는 개발자를 빠르게 하는가 | GitHub/Accenture는 PR 증가와 만족도 증가를 보고했다 | METR는 숙련 개발자가 느려질 수 있다고 보고했다 | 쉬운 반복 업무와 복잡한 고맥락 업무를 나눠야 한다 |
| 에이전트에 업무 앱 권한을 줘도 되는가 | 제품들은 브라우저, 파일, 앱 연결을 강화하고 있다 | 보안 문서는 샌드박스와 승인을 강조한다 | 읽기와 초안 생성부터 시작하고 실행 권한은 늦게 연다 |
| 법무/구매/재무도 자동화할 수 있는가 | 문서 검토와 자료 수집 병목이 크다 | 환각, fraud, 감사 리스크가 크다 | 자동 실행이 아니라 승인 패킷 생성이 맞다 |

## 근거 신뢰도 요약

| 주장 | 근거 성격 | 확신도 | 어떻게 써야 하는가 |
| --- | --- | --- | --- |
| 검토 가능한 산출물 중심 운영이 안전하다 | OpenAI/Anthropic/Google/GitHub 문서와 보안 자료가 일치 | 높음 | 강한 원칙으로 사용 |
| 개발/IT 파일럿이 가장 먼저다 | 제품 기능과 PR/CI 체계가 직접 맞음 | 높음 | 첫 PoC 후보로 사용 |
| 구매/법무/재무도 고가치다 | 인접 사례와 업무 구조가 맞음 | 중상 | 승인 패킷 중심으로 사용 |
| 벤더 사례의 절감 수치 | 고객사례는 많지만 독립 감사는 제한적 | 중간 | 가능성 예시로만 사용 |
| 제품별 우열 | 동일 조건 공개 비교가 부족 | 낮음 | 내부 benchmark 필요 |
| 장기 운영 ROI | 직접 결합 사례와 6-12개월 데이터 부족 | 낮음 | 파일럿에서 직접 측정 |

## 리서치 한계

이번 리서치는 유즈케이스와 실행안을 만드는 데는 충분하다. 그러나 "검증된 ROI 상위 10개"를 말하기에는 아직 부족하다. 특히 Codex/Claude Code와 n8n류 도구를 결합해 6-12개월 운영한 독립 사례는 공개 근거가 제한적이다.

또한 OpenAI, Anthropic, Google/Gemini 계열 제품을 같은 업무, 같은 권한, 같은 비용으로 비교한 공개 자료도 부족하다. 제품 선택은 공개 벤치마크보다 내부 업무 샘플로 직접 테스트하는 편이 맞다.

## 후속 질문

1. 우리 조직에서 반복 업무 30개를 뽑으면, 어떤 업무가 "초안/패킷/PR"으로 바뀔 수 있는가?
2. Codex와 Claude Code 중 어느 쪽이 우리 코드, 문서, 업무 시스템에서 더 잘 작동하는가?
3. n8n을 자체 호스팅할 것인가, Zapier/Make/Power Automate 같은 SaaS를 쓸 것인가?
4. 어떤 업무는 API로 연결하고, 어떤 업무는 화면 조작이나 수동 승인으로 남겨야 하는가?
5. 승인자가 감당할 수 있는 리뷰량은 어느 정도인가?

## 출처와 검색 깊이 요약

주요 근거는 다섯 묶음이다.

- 자동화 사례: [n8n case studies](https://n8n.io/case-studies/), [Microsoft customer stories](https://www.microsoft.com/en/customers), [Zapier customer stories](https://zapier.com/customer-stories), [Make success stories](https://www.make.com/en/success-stories)
- 에이전트 제품 방향: [OpenAI Codex](https://openai.com/codex/), [OpenAI Codex use cases](https://developers.openai.com/codex/use-cases), [Anthropic Claude Code](https://www.anthropic.com/product/claude-code), [Google Gemini Enterprise](https://cloud.google.com/gemini-enterprise)
- 워크플로우 구조: [n8n AI Agent Tool](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolaiagent/), [LangGraph human-in-the-loop](https://docs.langchain.com/oss/python/langgraph/human-in-the-loop), [GitHub Actions approvals](https://docs.github.com/en/actions/how-tos/deploy/configure-and-manage-deployments/control-deployments)
- 보안과 통제: [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/), [NIST GenAI Profile](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence), [Claude Code security](https://code.claude.com/docs/en/security)
- 반례와 한계: [METR 2025 OSS developer study](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/), [Stanford HAI legal hallucination](https://hai.stanford.edu/news/ai-trial-legal-models-hallucinate-1-out-6-or-more-benchmarking-queries), [RAND AI project failure report](https://www.rand.org/content/dam/rand/pubs/research_reports/RRA2600/RRA2680-1/RAND_RRA2680-1.pdf)

검색은 실제 사례, 프런티어 AI 회사 방향, 워크플로우 아키텍처, 직무별 유즈케이스, 거버넌스/ROI 리스크의 다섯 관점으로 나눠 수행했다. 긍정 사례와 실패 사례를 함께 보았고, 벤더 발표 수치는 가능성 근거로만 사용했다.
