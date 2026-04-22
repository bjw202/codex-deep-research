# 직무별 use case ideation + 근거 연결 - Codex/Claude Code 기반 고가치 업무 자동화

**Researcher**: R4  
**Mode**: mixed  
**Date**: 2026-04-23  
**Scope**: 업무공통, 개발/IT, 산업운영, 경영지원, 법무, 구매 영역에서 Codex, Claude Code, GitHub Copilot coding agent, workflow automation, RPA/IDP, enterprise AI agent를 조합해 만들 수 있는 고가치 유즈케이스를 설계한다. 단순 이메일 요약, 회의록 요약, 일반 질의응답처럼 가치가 낮거나 산출물 검증이 약한 사례는 제외한다. 최종 synthesis가 아니라 R4 관점의 bounded Researcher 산출물이다.

## 핵심 요약

- 결론: 고가치 유즈케이스는 "AI가 대신 말해준다"가 아니라 "에이전트가 시스템을 읽고, 파일/코드/데이터 산출물을 만들고, 검증 로그를 남긴 뒤 사람이 승인한다"는 구조에서 나온다. Codex use cases, Claude Code, GitHub Copilot coding agent, Siemens Industrial Copilot, finance ERP agent 연구가 모두 이 방향을 지지한다.
- 적용 조건: 후보는 최소 6개 업무영역(공통, 개발/IT, 산업운영, 경영지원, 법무, 구매)을 덮고, 각 영역마다 직접 근거 또는 인접 근거를 연결했다. 가장 강한 후보는 기존 시스템이 이미 있고 병목이 수작업 검토, 예외 처리, 코드/문서 변경, 데이터 대조에 있는 경우다.
- Top 10: 1순위는 개발/IT의 issue-to-PR와 보안/운영 triage, 2순위는 구매 supplier onboarding과 contract redline, 3순위는 재무 close/expense exception, 산업 maintenance/quality, 전사 보고 패키지다. 이들은 산출물이 PR, exception case, 승인 memo, work order, redline, audit packet처럼 검토 가능하다.
- 가장 큰 반례: legal AI hallucination, procurement data quality failure, RPA governance failure, AI code security, enterprise AI adoption barrier 검색에서 공통 실패 원인은 과도한 자율성, 데이터 품질, 권한 경계 부재, 검증 없는 자동 실행, ROI 불명확성으로 수렴했다.
- 더 좋은 문제 정의: "어디에 AI를 쓸까"보다 "어떤 반복 업무를 리뷰 가능한 산출물, 자동 검증, 승인 게이트가 있는 agentic workflow로 바꿀까"가 더 정확한 질문이다.

## 읽는 법

이 문서는 최종 전략 보고서가 아니라 후보 설계 저장소다. Top 10 표는 투자 우선순위를 빠르게 고르기 위한 것이고, 전체 후보 표는 각 직무 담당자가 자신의 시스템 환경에 맞게 PoC 범위를 자르는 데 쓴다. 효과 수치는 출처별 측정 단위가 다르므로 서로 직접 비교하면 안 된다. vendor-only(벤더나 고객사가 직접 발표한 자료)는 방향성 근거로만 쓰고, 운영 설계는 NIST, OWASP, COSO, GitHub responsible use 같은 통제 근거로 보정했다.

## 주요 발견

### 1. 고가치 후보는 산출물과 승인점이 명확한 업무에 몰린다

Codex 공식 use cases는 PR 리뷰, 데이터 분석 보고서, 슬라이드, bug triage, Computer Use QA, workflow skill 저장을 제시한다. Claude Code와 GitHub Copilot coding agent도 GitHub Actions, PR, issue, MCP, human review를 중심 workflow로 둔다. 그래서 고가치 업무는 "초안 생성"보다 "변경안, 검증 로그, 승인 패킷"으로 끝나는 작업이어야 한다.

### 2. 직무별로 가장 좋은 시작점은 다르다

개발/IT는 repo, CI, PR이 이미 검증 장치라 가장 바로 적용할 수 있다. 구매와 법무는 자동 실행보다 risk packet, redline, sourcing memo처럼 사람이 최종 판단하는 형태가 적합하다. 산업운영과 경영지원은 CMMS, ERP, QMS, AP, close system처럼 기존 시스템과 연결되면 가치가 크지만, 잘못 실행했을 때 물리 운영, 재무 통제, 감사 리스크가 커진다.

### 3. 코딩 에이전트의 차별점은 일반 업무도 "업무 코드"로 만들 수 있다는 점이다

Codex/Claude Code는 문서 작성 도구가 아니라 repository, shell, file, browser, API, MCP, GitHub Actions를 다룬다. 이 능력을 구매 RFP 템플릿, 법무 clause playbook, 월마감 reconciliation, 산업 work order, 보고서 생성 스크립트에 붙이면 반복 업무가 skill, workflow, runbook, validation script로 축적된다. 단, prompt만 저장하는 방식은 재현성이 낮으므로 입력 스키마, 금지 액션, 자동 검증, 승인 조건까지 묶어야 한다.

### 4. 실패 검색은 "완전자율"보다 bounded autonomy를 지지한다

법무에서는 생성AI가 만든 가짜 판례 인용으로 제재 사례가 계속 발생했고, Stanford HAI/RegLab은 법률 RAG 도구도 환각을 일으킨다고 보고했다. 구매에서는 supplier data quality, ERP/contract system fragmentation, governance misalignment가 반복 실패 원인으로 지목된다. OWASP는 LLM agent의 excessive agency, prompt injection, over-privileged tools를 주요 위험으로 본다. 따라서 자동화 설계는 read-only 수집, draft/patch 생성, deterministic validation, human approval, audit log를 기본값으로 둬야 한다.

## Top 10 우선순위

우선순위는 가치, 구현 가능성, 검증 가능성, 위험 통제 가능성, Codex/Claude Code 적합성을 함께 봤다. 높은 순위일수록 "바로 PoC를 시작해도 산출물과 승인점이 분명한" 후보에 가깝다.

| 순위 | 후보 ID | 업무영역 | 유즈케이스 | 왜 우선인가 | 핵심 근거 | 주요 승인점 |
| ---: | --- | --- | --- | --- | --- | --- |
| 1 | D1 | 개발/IT | Issue-to-PR, 테스트, 문서, 소규모 변경 자동화 | repo/CI/PR라는 검증 체계가 이미 있고 Codex, Claude Code, Copilot coding agent의 기본 사용처와 직접 일치 | OpenAI Codex use cases, GitHub Copilot coding agent, agentic PR 연구 | PR 리뷰, CI 통과, 독립 승인 |
| 2 | D3 | 개발/IT | 보안/운영 alert triage와 remediation PR/runbook | SecOps live operations 연구에서 productivity gain 근거가 있고, 읽기 중심 triage에서 시작 가능 | arXiv SOC/live operations, OWASP, NIST | 보안 담당자 승인, change window 승인 |
| 3 | P1 | 구매 | Supplier onboarding, KYC, sanctions, bank-account validation packet | procurement 병목이 수작업 chasing과 데이터 품질에 집중되어 있고, 자동 결정보다 검증 패킷 생성이 안전 | McKinsey procurement AI, TealBook, procurement challenge 자료 | 구매/법무/AP 승인, bank change 이중 승인 |
| 4 | L1 | 법무 | 계약 redline, clause playbook 적용, 협상 이슈표 | Gartner legal GenAI use cases와 CLM use case에 직접 맞고, 법무가 승인하는 redline 산출물로 제한 가능 | Gartner legal, Deloitte legal, Stanford legal hallucination 반례 | 변호사 최종 승인 |
| 5 | F1 | 경영지원 | 월마감 variance, account reconciliation, flux analysis 패키지 | ERP/BI 데이터와 증빙 대조가 반복 병목이고, COSO 내부통제와 잘 결합 가능 | COSO GenAI controls, FinRobot, OpenAI enterprise AI | 회계 owner 승인, controller sign-off |
| 6 | I2 | 산업운영 | Maintenance work order assistant와 troubleshooting packet | McKinsey와 Siemens가 maintenance/plc troubleshooting을 명시하고, 숙련자 부족 병목이 큼 | McKinsey maintenance, Siemens Industrial Copilot | 현장 supervisor 승인, 안전 승인 |
| 7 | F2 | 경영지원 | Expense/AP exception resolution automation | IDP+GenAI+automation agent 연구가 직접 사례를 제공하고, 완전자동보다 예외 큐 축소에 적합 | arXiv expense processing, FinRobot | AP 담당자 승인, 예외 지급 승인 |
| 8 | C1 | 업무공통 | 경영회의/이사회 보고 패키지 자동 생성 및 근거 대조 | 단순 PPT 생성이 아니라 KPI, 재무, 리스크, action owner를 자동 대조하는 고가치 보고 업무 | OpenAI Codex slide/data use cases, OpenAI enterprise AI | 보고 owner 승인, CFO/PMO 확인 |
| 9 | I3 | 산업운영 | 품질 nonconformance root cause와 CAPA packet | QMS, MES, ERP, 현장 로그를 묶어 원인 후보와 CAPA 초안을 만들 수 있고 감사 산출물이 남음 | Deloitte use cases, McKinsey operations, AI QA concerns | 품질 manager 승인, CAPA board 승인 |
| 10 | P2 | 구매 | RFP/RFQ 응답 정규화, 평가표, award memo | sourcing 업무의 비교/정규화/감사 trail 병목을 줄이고, 낙찰 판단은 사람이 유지 가능 | McKinsey procurement AI, procurement AI challenge 자료 | sourcing committee 승인, COI 확인 |

## 전체 후보 설계

아래 후보는 최소 15개 조건을 넘기기 위해 18개로 만들었다. 각 후보는 대상 업무, 기존 병목, 에이전트 역할, 연결 시스템, 산출물, 인간 승인점, 기대효과, 위험을 모두 포함한다.

| ID | 업무영역 | 대상 업무 | 기존 병목 | 에이전트가 하는 일 | 필요한 연결 시스템 | 산출물 | 인간 승인점 | 기대효과 | 위험 | 근거 연결 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| C1 | 공통 | 경영회의, 이사회, PMO 보고 패키지 | KPI, 재무, 프로젝트, 리스크 데이터가 Excel, BI, 문서, 티켓에 흩어져 수작업 취합과 버전 오류가 발생 | ERP/BI/Jira/Sheets에서 데이터 수집, 전월 대비 variance 계산, 출처 링크 포함 slide deck 생성, 숫자 reconciliations와 action owner 표 생성 | ERP, BI, Jira/Linear, Google Drive/SharePoint, PowerPoint, Git repo for templates | `.pptx`, KPI reconciliation log, issue/action register, source map | 보고 owner가 수치와 narrative 승인, CFO/PMO가 최종 배포 승인 | 보고 준비 시간 축소, 수치 출처 추적, 후속 action 누락 감소 | 잘못된 데이터 연결, 오래된 파일 참조, narrative 과잉 확신 | Codex slide/data use cases, OpenAI enterprise AI |
| C2 | 공통 | 정책/절차 변경 영향 분석과 workflow skill 패키징 | 규정, SOP, 템플릿, 시스템 권한이 따로 관리되어 변경 영향 파악이 느림 | 변경 문서를 읽고 영향받는 SOP, checklist, form, training item을 찾음. 반복 절차를 Codex/Claude skill 또는 workflow로 패키징하고 테스트 예제를 생성 | 문서관리시스템, Confluence/Notion, Git, LMS, Slack/Teams | 영향 분석표, 수정 PR, skill/workflow package, 검증 checklist | process owner와 compliance owner 승인 | 변경 반영 속도 향상, 표준 업무 재사용, 감사 대응성 향상 | 오래된 문서 기준으로 잘못된 변경 제안, 권한 없는 workflow 실행 | Codex Skills, COSO GenAI controls, NIST AI RMF |
| C3 | 공통 | 입사/전보/퇴사 onboarding/offboarding 통제 패킷 | HRIS, IAM, Jira, SaaS admin, 교육 이수 상태가 분산되어 누락 발생 | HR 이벤트를 기준으로 계정/권한/장비/교육 task 생성, 예외와 미완료 항목 추적, 종료 시 접근권 회수 evidence 수집 | HRIS, IAM/SSO, ITSM, MDM, LMS, Slack/Teams | onboarding tracker, access delta, exception report, evidence packet | HRBP, IT admin, manager 승인. 권한 부여는 시스템 owner 승인 | 누락 감소, 감사 evidence 자동화, 신규 구성원 ramp-up 단축 | 과도한 권한 추천, 개인정보 노출, manager 승인 우회 | OpenAI enterprise AI, NIST governance, RPA governance 검색 |
| D1 | 개발/IT | issue-to-PR, 테스트, 문서, 소규모 기능/버그 수정 | 개발자가 사소하지만 context-heavy한 티켓, 테스트 보강, 문서 업데이트에 많은 시간을 씀 | issue 분석, repo 탐색, 변경 계획, branch/PR 생성, 테스트/린트 실행, 리뷰 반영, changelog/doc 업데이트 | GitHub/GitLab, CI, test runner, issue tracker, package registry | PR, test results, implementation note, rollback note | reviewer 승인, CI 통과, branch protection | cycle time 단축, backlog 처리, 테스트/문서 부채 감소 | 보안 취약 코드, context 오해, multi-repo 한계, unsigned commits | GitHub Copilot coding agent, Claude Code GitHub Actions, arXiv agentic PR |
| D2 | 개발/IT | legacy migration, dependency upgrade, API/model upgrade | migration guide 해석, 반복 수정, 테스트 실패 대응, deprecation tracking이 수작업 | dependency diff 확인, migration checklist 작성, 단계별 PR, 자동 테스트, breaking change report 생성 | Git repo, CI, dependency scanner, OpenAPI docs, release notes | migration PR set, compatibility matrix, test failure report | tech lead 승인, security owner 승인 | 보안 패치와 버전 업그레이드 지연 감소 | transitive dependency 리스크, silent behavior change | Codex code migration/API upgrade use cases, GitHub responsible use |
| D3 | 개발/IT | SecOps alert triage, DLP/device policy conflict, remediation PR/runbook | alert가 많고 analyst가 로그 조회, severity 판단, runbook 갱신을 반복 | SIEM/EDR 로그 요약, 유사 incident 검색, 원인 가설, containment checklist, IaC/config PR 또는 runbook update 초안 생성 | SIEM, EDR, ticketing, Git repo, cloud logs, CMDB | triage packet, severity recommendation, remediation PR, runbook diff | security analyst 승인, change manager 승인 | MTTR 감소, reopen 감소, 반복 대응 표준화 | prompt injection, secret exposure, over-remediation | live SecOps 연구, NIST, OWASP |
| I1 | 산업운영 | PLC/automation code troubleshooting과 change request | 숙련 automation engineer 부족, 설비별 PLC 코드와 오류 메시지 해석이 어렵고 문서화가 늦음 | PLC 코드/알람/설비 문서 분석, 오류 원인 후보, safe change suggestion, Teamcenter/Jira change request 생성 | PLC code repo, SCADA/MES logs, Teamcenter/PLM, CMMS, Git | troubleshooting memo, code diff suggestion, change request, test checklist | automation engineer, safety engineer, production supervisor 승인 | downtime 원인 분석 단축, 숙련자 지식 전파 | 물리 안전 리스크, 오래된 설비 문서, 잘못된 코드 제안 | Siemens Industrial Copilot, Microsoft-Siemens case |
| I2 | 산업운영 | 설비 maintenance planning, work order, 현장 troubleshooting | 매뉴얼, 과거 정비 이력, 센서 데이터, 작업자 노트가 분산되어 계획/진단이 느림 | failure symptom 수집, manual/RCA history 검색, parts availability 확인, work order와 step-by-step checklist 초안 생성 | CMMS/EAM, IoT historian, parts inventory, manuals, shift logs | work order draft, diagnostic tree, required parts list, safety checklist | maintenance supervisor와 safety officer 승인 | MTTR/계획 정비 효율 개선, junior technician 지원 | 안전 절차 누락, sensor data 품질, 부품 재고 오류 | McKinsey maintenance, Deloitte maintenance use case |
| I3 | 산업운영 | 품질 nonconformance, RCA, CAPA packet | MES/QMS/ERP/검사 데이터와 현장 사진/로그를 모아 원인 분석 문서 만드는 시간이 길다 | 불량 lot 추적, 공정 조건 비교, 유사 CAPA 검색, 5-Why/Fishbone 초안, containment action 생성 | QMS, MES, ERP, LIMS, image store, supplier quality portal | NCR summary, RCA draft, CAPA packet, evidence bundle | quality manager, process engineer, CAPA board 승인 | 재발 방지 조치 속도 향상, 감사 대응성 향상 | 상관관계를 원인으로 오판, supplier blame 편향 | Deloitte AI use cases, McKinsey operations, QA4AI 연구 |
| F1 | 경영지원 | 월마감 variance, reconciliation, flux analysis | ERP, subledger, spreadsheet, BI 수치가 맞지 않고 설명 narrative 작성이 반복됨 | 계정별 variance threshold 적용, source transaction 샘플링, reconciliation script 실행, flux narrative 초안 생성 | ERP, subledger, data warehouse, Excel, close management tool | reconciliation workbook, variance memo, exception list, audit trail | account owner, controller 승인 | close cycle 단축, 수치 추적성 개선, audit query 대응 | 회계 판단 자동화 오남용, spreadsheet control 누락 | COSO GenAI controls, FinRobot, OpenAI enterprise AI |
| F2 | 경영지원 | Expense/AP invoice exception 처리 | OCR/IDP 후에도 match exception, missing receipt, policy exception이 많아 AP 담당자가 수작업 확인 | 영수증/PO/invoice/정책 대조, exception reason 분류, supplier/employee follow-up draft, 승인 큐 정리 | ERP/AP, expense tool, OCR/IDP, procurement, email, policy repo | exception case, missing-info request, payment hold recommendation | AP 담당자, budget owner, compliance 승인 | manual touch 감소, 지급 지연 감소, policy leakage 감소 | 중복 지급, 잘못된 hold, 개인정보 처리 | expense processing case study, FinRobot |
| F3 | 경영지원 | Budget reforecast와 headcount/resource scenario | finance, HR, sales pipeline, project demand 데이터가 분산되어 scenario 반복 작성이 느림 | driver 수집, forecast model 실행, scenario assumptions 문서화, 민감도 표와 risk narrative 생성 | FP&A tool, HRIS, CRM, ERP, planning spreadsheet | forecast pack, assumption log, scenario comparison | FP&A lead, business owner 승인 | planning cycle 단축, assumption transparency | 모델이 과거 bias를 강화, 비공식 수치 사용 | OpenAI enterprise AI, McKinsey corporate functions |
| L1 | 법무 | 계약 redline, clause playbook, 협상 이슈표 | 표준 조항과 과거 협상 입장 찾기가 느리고 legal queue가 병목 | 계약서 clause 추출, playbook 기준 deviation 탐지, redline/comment draft, fallback position 제안 | CLM, document repository, clause library, CRM/procurement system | redline draft, issue list, risk score, negotiation memo | 변호사와 business owner 최종 승인 | 계약 검토 turnaround 감소, 일관성 향상 | hallucinated legal rationale, 특수 맥락 누락, privilege risk | Gartner legal GenAI, Deloitte legal, Stanford legal hallucination |
| L2 | 법무 | 법률 리서치와 소송/분쟁 memo | 판례/법령/증거 문서 확인이 오래 걸리고 citation 오류 위험이 큼 | 질문 범위 정의, authorized legal DB 검색, citation verification table, contrary authority 탐색, memo 초안 생성 | Westlaw/Lexis/공식 법령 DB, DMS, eDiscovery, matter management | citation-checked memo, authority table, evidence map | 담당 변호사 citation 전수 확인 후 사용 | research first draft 속도 향상, 누락 쟁점 탐지 | 가짜 판례/인용, 관할권 착오, 비밀정보 노출 | Stanford HAI, AP/ABA sanction cases |
| L3 | 법무 | 규제 변경 영향 분석과 내부통제 mapping | 법령/감독지침 변경이 policy, product, contract, control에 미치는 영향 추적이 느림 | 신규 규제 수집, 내부 policy/control 매핑, gap 분석, owner별 action item 생성 | regulatory feed, policy repo, GRC, Jira, DMS | impact memo, control mapping, remediation backlog | compliance/legal owner 승인 | 규제 대응 지연 감소, evidence trail 확보 | 규제 해석 오류, 지역별 차이 누락 | NIST AI RMF, COSO GenAI controls, legal AI use case 자료 |
| P1 | 구매 | Supplier onboarding, KYC, tax/bank/sanctions validation | supplier master data가 불완전하고 이메일 chasing, 중복 vendor, bank change fraud가 반복됨 | intake form validation, document extraction, sanctions/tax/bank rule checks, missing-doc follow-up draft, duplicate supplier 탐지 | Supplier portal, ERP vendor master, AP, sanctions/tax API, bank validation, CLM | onboarding case, risk packet, duplicate alert, approval checklist | procurement, AP, legal, risk 승인. bank change는 별도 2인 승인 | onboarding cycle 단축, fraud/data quality risk 감소 | 잘못된 supplier merge, 민감 데이터 노출, external API 오류 | McKinsey procurement AI, TealBook data quality, procurement failure 검색 |
| P2 | 구매 | RFP/RFQ 응답 정규화, 비교 평가, award memo | 공급사 제안서 형식이 달라 비교가 어렵고 평가 근거와 COI trail이 약함 | bid response 파싱, 요구사항 충족도 매트릭스, TCO/리스크 비교, clarification question 초안, award memo 작성 | eSourcing, ERP spend, CLM, supplier portal, market data | evaluation matrix, TCO model, clarification list, award memo | sourcing committee, legal, finance 승인 | sourcing cycle 단축, 평가 일관성, 감사 trail 강화 | supplier bias, scoring 기준 불투명, hallucinated claim | McKinsey procurement AI, procurement challenge 자료 |
| P3 | 구매 | Spend/category analytics와 savings opportunity backlog | spend taxonomy가 깨지고 공급사 hierarchy가 불완전해 savings 후보가 늦게 발견됨 | vendor/commodity normalization, maverick spend 탐지, consolidation 후보, should-cost/market signal 조회, savings backlog 생성 | ERP/AP, procurement analytics, supplier master, contract repo, market data | category insight pack, savings backlog, data-quality issue list | category manager와 finance validation | hard savings 후보 발굴, maverick spend 감소 | 잘못된 분류, 환율/단가 기준 오류, 데이터 품질 의존 | McKinsey procurement AI, DPW/TealBook data quality |

## 영역별 근거 연결

각 영역은 최소 1개 이상의 근거 출처로 연결했다. 단, 법무와 구매는 실패 리스크가 강하므로 use case 근거와 반례 근거를 함께 적었다.

| 업무영역 | 적용 논리 | 대표 근거 | 확신도 |
| --- | --- | --- | --- |
| 공통 | Codex는 slide deck, dataset analysis, workflow skills, Computer Use를 공식 use case로 제시한다. 전사 보고, 정책 변경, onboarding처럼 파일과 시스템을 오가는 업무에 맞다. | OpenAI Codex use cases, Codex Skills, OpenAI State of Enterprise AI | 높음 |
| 개발/IT | repo, CI, PR, issue tracker가 이미 agent output과 검증 loop를 제공한다. agentic PR 연구는 성공률과 실패 유형을 동시에 보여준다. | GitHub Copilot coding agent docs, Claude Code GitHub Actions, arXiv agentic PR studies | 높음 |
| 산업운영 | Siemens/Microsoft와 McKinsey는 industrial copilot, PLC troubleshooting, maintenance planning을 직접 사례로 제시한다. 현장 안전 승인 없이는 자동 실행하면 안 된다. | Siemens Industrial Copilot, Microsoft-Siemens case, McKinsey maintenance | 중상 |
| 경영지원 | ERP/finance process는 structured data와 unstructured evidence가 섞인 cross-functional workflow라 agent와 IDP/RPA 결합에 적합하다. COSO 관점의 내부통제 설계가 필요하다. | FinRobot, expense automation case study, COSO GenAI controls | 중상 |
| 법무 | 계약, 법률 리서치, 규제 영향 분석은 GenAI 후보가 많지만 hallucination과 professional responsibility 리스크가 크다. citation verification과 변호사 승인 없이는 사용하면 안 된다. | Gartner legal GenAI, Deloitte legal, Stanford HAI legal hallucination, AP/ABA sanction reports | 중상 |
| 구매 | procurement AI는 spend, sourcing, supplier risk에 가치가 있지만 supplier master data와 ERP/CLM fragmentation이 실패 원인이다. data quality workflow부터 시작해야 한다. | McKinsey procurement AI, TealBook, TechTarget, procurement AI failure searches | 중상 |

## 근거 표

| 주장 | 근거 | 출처 유형 | 확신도 | URL |
| --- | --- | --- | --- | --- |
| Codex/코딩 에이전트는 일반 업무 자동화에도 적용 가능하다 | Codex use cases가 PR, bug triage, slide decks, dataset/report, inbox, Computer Use, skills를 공식적으로 제시한다 | official / primary | 높음 | https://developers.openai.com/codex/use-cases |
| 반복 업무는 prompt가 아니라 skill/workflow package로 저장해야 한다 | Codex Skills는 instructions, resources, scripts, assets를 묶는 재사용 형식이다 | official / primary | 높음 | https://developers.openai.com/codex/skills |
| GitHub coding agent는 PR 생성과 사람 승인 중심으로 설계되어 있다 | Copilot coding agent는 branch/PR를 만들 수 있지만 approve/merge는 못 하고 Actions 실행도 사용자 승인이 필요하다 | official / primary | 높음 | https://docs.github.com/en/copilot/concepts/about-assigning-tasks-to-copilot |
| Claude Code는 GitHub Actions와 MCP를 통해 workflow automation에 붙을 수 있다 | Anthropic 문서는 Claude Code GitHub Action, secrets, permissions, MCP config를 설명한다 | official / primary | 높음 | https://docs.anthropic.com/en/docs/claude-code/github-actions |
| 개발/IT 자동화는 task별 성능 차이를 전제로 해야 한다 | arXiv agentic PR 연구가 여러 coding agent의 PR acceptance와 실패 유형을 task별로 분석한다 | academic | 중상 | https://arxiv.org/abs/2602.08915 / https://arxiv.org/abs/2601.15195 |
| SecOps와 endpoint operations는 GenAI가 생산성 지표를 개선할 가능성이 있다 | live operations 연구가 security incident MTTR, DLP alert classification, device policy conflict resolution 등 운영 지표 개선을 분석한다 | academic / experiment | 중상 | https://arxiv.org/abs/2411.03116 / https://arxiv.org/abs/2504.08805 |
| 산업 maintenance와 PLC troubleshooting은 GenAI/industrial copilot 후보가 직접 존재한다 | Siemens Industrial Copilot은 automation engineering, maintenance, error handling, Teamcenter change request를 다룬다 | direct case / vendor | 중상 | https://www.siemens-advanta.com/default/cases/industrial-copilot |
| McKinsey는 산업 maintenance에서 troubleshooting, planning, scheduling, repair 지원을 유망 use case로 본다 | maintenance 문서가 숙련자 부족, 이종 설비, virtual agent, unplanned downtime 대응을 설명한다 | reliable / consulting | 중상 | https://www.mckinsey.com/capabilities/operations/our-insights/rewiring-maintenance-with-gen-ai |
| finance ERP agent는 reimbursement와 wire transfer 같은 cross-functional workflow에 적용 가능하다 | FinRobot은 ERP finance agent framework와 employee reimbursements, bank wire transfer case를 제시한다 | academic | 중상 | https://arxiv.org/abs/2506.01423 |
| expense/AP exception은 IDP+GenAI+automation agent 결합의 직접 후보이다 | corporate expense processing case study가 IDP와 automation agent 기반 E2E 자동화를 다룬다 | academic / case | 중상 | https://arxiv.org/abs/2505.20733 |
| GenAI 내부통제는 use case inventory, key controls, upstream data, interfaces까지 관리해야 한다 | COSO GenAI publication은 GenAI risks and controls를 내부통제 관점으로 정리한다 | standard / framework | 높음 | https://www.coso.org/generative-ai |
| 법무 부서는 GenAI use case를 검토하되 hallucination 통제를 핵심으로 둬야 한다 | Gartner는 legal departments의 GenAI use cases를 제시하고, Stanford HAI는 legal RAG tools도 hallucinate한다고 보고한다 | reliable + academic | 중상 | https://www.gartner.com/en/newsroom/press-releases/2025-02-19-gartner-identifies-the-top-6-use-cases-for-generative-ai-in-legal-departments / https://hai.stanford.edu/news/ai-trial-legal-models-hallucinate-1-out-6-or-more-benchmarking-queries |
| 법무 AI output은 변호사가 전수 검증해야 한다 | AP/ABA 보도는 fake citations로 sanction이 검토되거나 부과된 사례를 반복 보고한다 | direct failure case | 높음 | https://apnews.com/article/8cbaf729dafc2b56bee59545391707c0 / https://www.americanbar.org/groups/litigation/resources/litigation-news/2025/lawyer-sanctioned-failure-catch-ai-hallucination/ |
| 구매 AI는 spend, market, supplier risk 분석에 가치가 있다 | McKinsey는 procurement teams가 spend, market, specification data를 자연어로 질의하고 supplier distress 대체 source를 찾는 예를 든다 | reliable / consulting | 중상 | https://www.mckinsey.com/capabilities/operations/our-insights/revolutionizing-procurement-leveraging-data-and-ai-for-strategic-advantage |
| 구매 AI 실패는 supplier data quality와 system fragmentation에 크게 좌우된다 | TealBook, TechTarget, procurement AI articles가 data quality, governance, legacy integration, transparency를 반복 지적한다 | stakeholder / reliable | 중간 | https://www.tealbook.com/blog/why-ai-in-procurement-fails-without-reliable-supplier-data/ / https://www.techtarget.com/searcherp/tip/5-challenges-of-using-AI-in-procurement |
| agentic automation은 excessive agency와 prompt injection을 통제해야 한다 | OWASP LLM Top 10 2025는 excessive agency, prompt injection, tool use risk를 제시한다 | standard | 높음 | https://owasp.org/www-project-top-10-for-large-language-model-applications/ |
| enterprise AI adoption은 pilot 이후 scale과 ROI에서 막히기 쉽다 | Gartner는 GenAI project abandonment risk를, McKinsey는 enterprise-wide approach와 성공 배치 차이를 보고한다 | reliable / survey | 중상 | https://www.gartner.com/en/newsroom/press-releases/2024-07-29-gartner-predicts-30-percent-of-generative-ai-projects-will-be-abandoned-after-proof-of-concept-by-end-of-2025 / https://www.mckinsey.com/capabilities/operations/our-insights/gen-ai-in-corporate-functions-looking-beyond-efficiency-gains |
| OpenAI enterprise usage는 persistent workflow/GPT usage가 확대되고 있음을 보여준다 | OpenAI State of Enterprise AI는 고객 usage, BBVA legal chatbot 등 enterprise workflow 사례를 제시한다 | stakeholder / aggregated usage | 중상 | https://openai.com/business/guides-and-resources/the-state-of-enterprise-ai-2025-report/ |
| AI agent/RPA형 자동화는 audit trail, exception handling, governance가 없으면 실패한다 | GSA RPA playbook과 NIST AI RMF는 governance, oversight, risk management 구조를 요구한다 | government / standard | 높음 | https://www.gsa.gov/system/files/rpa-playbook-ic-addendum-v10.pdf / https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence |

## 출처 품질 매트릭스

| 출처 유형 | 개수 | 핵심 기여 | 약점 |
| --- | ---: | --- | --- |
| official / primary | 8 | OpenAI Codex, Anthropic Claude Code, GitHub Copilot, NIST, COSO, GSA 등 기능과 통제 기준 확인 | 벤더 문서는 장점 중심이며 실제 실패율을 덜 보여줌 |
| academic / standard / patent | 9 | agentic PR, SecOps live operations, finance ERP agent, expense automation, legal hallucination, NIST/OWASP/COSO 통제 근거 제공 | 일부 arXiv는 peer review 전이며 일반 업무 전체로 바로 일반화하기 어려움 |
| direct case / experiment | 7 | Siemens Industrial Copilot, SOC live operations, expense processing, FinRobot, GitHub coding agent workflow, legal sanction 사례 | 고객 사례는 vendor-reported인 경우가 많고 독립 감사 수치가 부족 |
| vendor / stakeholder | 6 | 제품 기능, use case 범위, customer examples, supplier data quality issue 확인 | ROI 수치와 성공 사례 편향 가능 |
| community | 5 | procurement data mess, automation silent failure, Copilot/Claude operational friction 확인 | 익명/비대표 자료라 핵심 결론에는 보조로만 사용 |
| weak / unverified | 2 | 최신 adoption friction과 hype 반례 탐색 보조 | 정량 결론에는 사용하지 않음 |

## 반례/실패 사례 검색 로그

필수 반례 쿼리 5개를 포함해 검색했다. 결론은 "하지 말자"가 아니라 "자동 실행하지 말고 검토 가능한 산출물과 승인 게이트로 제한하자"다.

| 쿼리 | 목적 | 결과 | 결론 영향 |
| --- | --- | --- | --- |
| `legal AI hallucination` | 법무 자동화의 치명 실패 확인 | Mata v. Avianca 이후 fake citation sanction 사례가 반복 보도. AP는 2025년 Alabama prison case에서 존재하지 않는 citation으로 sanction 검토 사례를 보도. Stanford HAI는 legal RAG tools도 benchmark에서 hallucination을 보인다고 설명 | L2 법률 리서치는 citation verification table과 변호사 전수 확인 없이는 불가 |
| `procurement automation failure` | 구매 자동화 실패 원인 확인 | supplier data quality, fragmented ERP/CLM/supplier portals, governance misalignment, change resistance가 반복 원인으로 등장 | P1/P3는 자동 sourcing decision보다 supplier data cleanup, validation packet, approval trail부터 시작 |
| `RPA governance` | workflow/RPA형 자동화 통제 확인 | GSA RPA playbook은 automation scale, audit/accountability, enterprise governance를 강조. RPA bot sprawl과 exception handling 실패가 위험으로 반복됨 | 모든 후보에 owner, audit log, exception queue, kill switch를 요구 |
| `AI code security` | coding agent의 보안 실패 가능성 확인 | OWASP LLM Top 10은 prompt injection, insecure output handling, excessive agency를 제시. GitHub responsible use는 sensitive info exposure, firewall, branch 제한, Actions approval을 설명 | D1/D2/D3는 least privilege, branch protection, CI/security scan, human review 필수 |
| `enterprise AI adoption barrier` | PoC 이후 확산 실패 원인 확인 | Gartner는 poor data quality, inadequate risk controls, escalating costs, unclear business value 때문에 GenAI project abandonment를 예측. McKinsey는 enterprise-wide approach가 단일 BU/지역 접근보다 배포 성공률이 높다고 보고 | Top 10은 ROI가 보이는 반복 업무와 governance가 쉬운 산출물 중심으로 선정 |
| `legal AI fake citations sanction 2025` | 법무 반례 최신성 확인 | ABA, AP, Axios 등에서 fake citation sanction, judge warning, 변호사 책임을 반복 보도 | 법무 후보는 "AI final answer"가 아니라 "verified memo draft"로 제한 |
| `procurement AI data quality supplier master failure` | 구매 후보의 선결조건 확인 | TealBook, TechTarget, procurement community가 supplier master data 품질과 duplicate/vendor hierarchy 문제를 반복 지적 | P1을 P2/P3보다 우선순위 높게 배치 |
| `Copilot coding agent limitations content exclusions` | 개발/IT 자동화 한계 확인 | GitHub docs는 same repo, one PR, cannot approve/merge, content exclusions 미반영, GitHub-hosted runners 등 제한을 명시 | D1/D2는 multi-repo, 민감 파일, signed commit 요구가 있으면 별도 설계 필요 |
| `AI agent excessive agency OWASP` | agentic workflow 보안 통제 확인 | OWASP는 tool/function 권한 과다, autonomous action, external system interface를 주요 위험으로 다룸 | 모든 후보에 read-only default, allowlist tools, human approval 적용 |
| `AI automation silent failure invoice workflow` | AP/구매 자동화의 조용한 실패 확인 | 커뮤니티와 AP automation 논의에서 input contract drift, missing tax ID, payment matching exception, silent sync failure가 반복됨 | F2/P1에는 completion logging, reconciliation, exception reason code가 필요 |

## 상충점과 불확실성

- **vendor 사례와 독립 근거의 강도가 다르다.** Siemens, OpenAI, GitHub, Anthropic, McKinsey 자료는 use case 방향을 잡는 데 유용하지만, ROI 수치와 성공률은 독립 검증이 약한 경우가 많다. 그래서 우선순위는 큰 생산성 수치보다 검증 가능한 산출물과 통제 가능성을 더 높게 반영했다.
- **일반 업무 자동화의 대규모 독립 실험은 아직 부족하다.** agentic PR, SecOps, finance process는 공개 연구가 있으나, 경영회의 deck, supplier onboarding, contract redline의 대규모 공개 성과 연구는 제한적이다. 이 영역은 내부 baseline을 먼저 잡아야 한다.
- **법무와 구매는 자동화 가치가 크지만 승인 비용도 크다.** 계약 redline과 supplier risk packet은 고가치지만, hallucination, privilege, supplier bias, bank fraud 같은 실패 비용이 커서 full automation이 아니라 decision support가 맞다.
- **산업운영은 물리 안전 때문에 더 보수적으로 설계해야 한다.** Siemens/McKinsey 근거는 유망하지만, 현장 설비 제어와 안전 절차는 소프트웨어 PR보다 실패 비용이 크다. 제안과 change request 생성까지가 1차 범위다.
- **엔터프라이즈 확산의 병목은 모델 성능만이 아니다.** 데이터 권한, system integration, owner 부재, chargeback, audit, 사용자 교육, ROI 측정이 더 큰 병목일 수 있다.

## 의사결정 영향

1. 첫 PoC는 D1, D3, P1, L1, F1 중 조직 데이터 접근성이 가장 좋은 업무로 잡는 것이 합리적이다. 이 후보들은 산출물이 검토 가능하고 기존 시스템이 명확하며, 실패 시 되돌리기 쉽다.
2. 모든 후보에 공통 platform guardrail을 둬야 한다. 최소 요건은 tool allowlist, read-only 기본값, write action approval, audit log, source citation, validation script, exception queue, owner mapping이다.
3. 업무별 KPI는 사용량이 아니라 cycle time, 재작업률, exception 처리 시간, PR merge rate, false positive, 승인 반려율, 감사 query 감소, hard savings로 둔다.
4. procurement/legal/finance는 "AI가 최종 판단"하는 표현을 금지하고 "AI가 승인 패킷을 준비"하는 식으로 업무 정의를 바꿔야 한다.
5. repeated workflow는 skill 또는 workflow package로 저장한다. 입력 스키마, 허용 시스템, 금지 행동, 검증 명령, 승인 조건, 실패 시 중단 기준을 포함해야 한다.

## 인접 질문

- 조직 내부의 상위 30개 반복 업무를 "데이터 접근 가능성, 산출물 검증 가능성, 승인 owner 명확성, 실패 비용"으로 점수화하면 Top 10 순위가 어떻게 바뀌는가?
- Codex/Claude Code를 중앙 agent platform으로 둘 때, 어떤 연결은 MCP/API로 만들고 어떤 연결은 RPA/Computer Use로만 제한해야 하는가?

## 출처 목록

| # | 출처 | 날짜/버전 | 확신도 | URL |
| ---: | --- | --- | --- | --- |
| 1 | OpenAI Codex use cases | 2026-04-23 확인 | 높음 | https://developers.openai.com/codex/use-cases |
| 2 | OpenAI Codex Skills | 2026-04-23 확인 | 높음 | https://developers.openai.com/codex/skills |
| 3 | OpenAI State of Enterprise AI 2025 Report | 2025 report, 2026-04-23 확인 | 중상 | https://openai.com/business/guides-and-resources/the-state-of-enterprise-ai-2025-report/ |
| 4 | Anthropic Claude Code GitHub Actions | 2026-04-23 확인 | 높음 | https://docs.anthropic.com/en/docs/claude-code/github-actions |
| 5 | Anthropic Claude Code common workflows | 2026-04-23 확인 | 높음 | https://docs.anthropic.com/en/docs/claude-code/tutorials |
| 6 | GitHub Docs: About Copilot coding agent | 2026-04-23 확인 | 높음 | https://docs.github.com/en/copilot/concepts/about-assigning-tasks-to-copilot |
| 7 | GitHub Docs: Responsible use of Copilot coding agent | 2026-04-23 확인 | 높음 | https://docs.github.com/en/copilot/responsible-use-of-github-copilot-features/responsible-use-of-copilot-coding-agent-on-githubcom |
| 8 | Comparing AI Coding Agents: A Task-Stratified Analysis of Pull Request Acceptance | arXiv 2602.08915, 2026 | 중상 | https://arxiv.org/abs/2602.08915 |
| 9 | Where Do AI Coding Agents Fail? | arXiv 2601.15195, 2026 | 중상 | https://arxiv.org/abs/2601.15195 |
| 10 | Generative AI and Security Operations Center Productivity | arXiv 2411.03116, 2024 | 중상 | https://arxiv.org/abs/2411.03116 |
| 11 | Generative AI in Live Operations | arXiv 2504.08805, 2025 | 중상 | https://arxiv.org/abs/2504.08805 |
| 12 | Siemens Advanta Industrial Copilot case | 2026-04-23 확인 | 중상 | https://www.siemens-advanta.com/default/cases/industrial-copilot |
| 13 | Microsoft Source: Siemens and Microsoft scale industrial AI | 2024-10-24 | 중상 | https://news.microsoft.com/source/2024/10/24/siemens-and-microsoft-scale-industrial-ai/ |
| 14 | McKinsey: Rewiring maintenance with gen AI | 2025-02-06 | 중상 | https://www.mckinsey.com/capabilities/operations/our-insights/rewiring-maintenance-with-gen-ai |
| 15 | Deloitte Generative AI for Organizations | 2026-04-23 확인 | 중간 | https://www.deloitte.com/us/en/services/consulting/services/generative-ai.html |
| 16 | FinRobot: Generative Business Process AI Agents for ERP in Finance | arXiv 2506.01423, 2025 | 중상 | https://arxiv.org/abs/2506.01423 |
| 17 | E2E Process Automation Leveraging GenAI and IDP-Based Automation Agent | arXiv 2505.20733, 2025 | 중상 | https://arxiv.org/abs/2505.20733 |
| 18 | COSO: Achieving Effective Internal Control Over GenAI | 2026 publication page | 높음 | https://www.coso.org/generative-ai |
| 19 | Gartner: Top 6 Use Cases for GenAI in Legal Departments | 2025-02-19 | 중상 | https://www.gartner.com/en/newsroom/press-releases/2025-02-19-gartner-identifies-the-top-6-use-cases-for-generative-ai-in-legal-departments |
| 20 | Stanford HAI: Legal models hallucinate in benchmarking queries | 2024, 2026-04-23 확인 | 높음 | https://hai.stanford.edu/news/ai-trial-legal-models-hallucinate-1-out-6-or-more-benchmarking-queries |
| 21 | AP: Judge considers sanctions for AI court filings | 2025-05-21 | 높음 | https://apnews.com/article/8cbaf729dafc2b56bee59545391707c0 |
| 22 | ABA: Lawyer sanctioned for failure to catch AI hallucination | 2025, 2026-04-23 확인 | 높음 | https://www.americanbar.org/groups/litigation/resources/litigation-news/2025/lawyer-sanctioned-failure-catch-ai-hallucination/ |
| 23 | McKinsey: Revolutionizing procurement with data and AI | 2024, 2026-04-23 확인 | 중상 | https://www.mckinsey.com/capabilities/operations/our-insights/revolutionizing-procurement-leveraging-data-and-ai-for-strategic-advantage |
| 24 | TealBook: Why AI in procurement fails without supplier data | 2026, 2026-04-23 확인 | 중간 | https://www.tealbook.com/blog/why-ai-in-procurement-fails-without-reliable-supplier-data/ |
| 25 | TechTarget: 5 challenges of using AI in procurement | 2026, 2026-04-23 확인 | 중간 | https://www.techtarget.com/searcherp/tip/5-challenges-of-using-AI-in-procurement |
| 26 | OWASP Top 10 for LLM Applications | 2025 version, 2026-04-23 확인 | 높음 | https://owasp.org/www-project-top-10-for-large-language-model-applications/ |
| 27 | NIST AI RMF Generative AI Profile | 2024 | 높음 | https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence |
| 28 | GSA RPA Program Playbook Internal Controls Addendum | 2024, 2026-04-23 확인 | 중상 | https://www.gsa.gov/system/files/rpa-playbook-ic-addendum-v10.pdf |
| 29 | Gartner: 30% GenAI projects abandoned after PoC prediction | 2024-07-29 | 중상 | https://www.gartner.com/en/newsroom/press-releases/2024-07-29-gartner-predicts-30-percent-of-generative-ai-projects-will-be-abandoned-after-proof-of-concept-by-end-of-2025 |
| 30 | McKinsey: Gen AI in corporate functions | 2024, 2026-04-23 확인 | 중상 | https://www.mckinsey.com/capabilities/operations/our-insights/gen-ai-in-corporate-functions-looking-beyond-efficiency-gains |

## 검색 포화 판단

필수 깊이 게이트는 충족했다. 공식/1차 출처는 OpenAI, Anthropic, GitHub, NIST, COSO, GSA 등 2개 이상을 확보했고, 학술/표준 출처는 agentic PR, SecOps live operations, finance ERP agent, expense automation, NIST, OWASP, COSO로 2개 이상 확보했다. 직접 사례 또는 실험은 Siemens Industrial Copilot, Microsoft-Siemens, SecOps live operations, expense processing, FinRobot, GitHub coding agent workflow로 2개 이상 확보했다.

반례/실패 검색은 사용자가 지정한 `legal AI hallucination`, `procurement automation failure`, `RPA governance`, `AI code security`, `enterprise AI adoption barrier`를 모두 수행했다. 추가 검색에서도 새 증거 유형보다는 같은 실패 원인(데이터 품질, 권한, 검증, governance, ROI)이 반복되어 포화로 판단했다. 아직 부족한 항목은 특정 기업 내부에서 Codex/Claude Code를 구매/법무/재무 업무에 장기간 적용한 독립 성과 데이터이며, 다음 라운드에서는 내부 baseline이 있는 벤치마크 또는 감사 가능한 case study를 찾아야 한다.
