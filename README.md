# 이윤우

풀스택 개발자입니다. 서버는 Java·Spring과 Django, 화면은 React로 만듭니다.
만든 기능이 정말 버티는지 일부러 망가뜨려 보고 숫자로 확인하는 편입니다.

생명과학을 전공하다 컴퓨터학부를 복수전공했고, SSAFY 15기를 2026년 12월에 수료합니다.

메일 leeyw001013@naver.com

## 한눈에

| 프로젝트 | 기간 | 인원 | 맡은 일 | 숫자로 보면 |
|---|---|---|---|---|
| [AudiSay](https://github.com/luster-woo/AudiSay/blob/main/PORTFOLIO.md) | 2026.10–11 | 6명 | Spring 백엔드 | 브로커 장애 중 메시지 유실 50/50 → 0 |
| [FinFit](https://github.com/luster-woo/finance_pjt) | 2026.05–06 | 2명 | 팀장, Django 백엔드 전체 | 상품 조회 평균 4.5초 → 80ms |
| [SSabway](https://github.com/luster-woo/SSabway) | 2026.07–08 | 6명 | 프론트엔드, 관리자 앱 전담 | 관리자 API 9종 · 공통 프로젝트 우수상(팀) |
| [SOBI](https://github.com/luster-woo/Sobi/blob/develop/PORTFOLIO.md) | 2026.08–10 | 6명 | 프론트엔드 파트장 | 화면 22개 중 14개 · 특화 프로젝트 우수상(팀) |

숫자는 전부 직접 잰 값이고, 잰 방법은 각 저장소 문서에 적어 두었습니다.

## 프로젝트

### AudiSay · 시각장애인용 AI 화면해설

<img src="https://github.com/luster-woo/AudiSay/raw/main/docs/portfolio/audisay_chat.png" width="480" alt="AudiSay 재생 화면과 음성 챗봇">

영상 해설을 듣다가 "방금 누가 골 넣었어?" 하고 물으면 답해 주고 그 장면으로 옮겨 주는 서비스입니다. 해설 생성 작업 흐름, 해설 조회, 음성 챗봇, 인증 서류 OCR 쪽 Spring 서버를 맡았습니다.

- RabbitMQ를 40초 멈춰 보니 API는 정상인데 메시지 50개가 전부 사라졌습니다. Outbox로 바꾼 뒤 같은 실험에서는 0개
- 해설 조회 p95 562ms → 61ms. 의심했던 N+1이 아니라 음성 주소 서명 계산이 원인이었습니다
- 챗봇은 평가 문항 192개를 먼저 만들고 설계를 바꿔 가며 쟀습니다. 의도 분류 95.5% → 99.1%

로컬 측정이고 실사용자 데이터는 없습니다. 코드는 상당 부분 Claude와 함께 썼고, 구조와 대안 선택, 평가와 측정은 직접 했습니다. [자세히 보기](https://github.com/luster-woo/AudiSay/blob/main/PORTFOLIO.md)

### FinFit · 금융성향 기반 상품 추천

<img src="https://github.com/luster-woo/finance_pjt/raw/master/screenshots/thumb/13_test_result.png" width="480" alt="FinFit 금융성향 검사 결과와 추천">

금융성향 검사 결과로 예·적금, 주식, 카드를 추천해 주는 서비스입니다. 2인 팀의 팀장으로 Django 백엔드 전체를 맡았습니다.

- 상품을 열 때마다 부르던 금융감독원 API를 관리자 수집 API로 옮겨 평균 4.5초 → 80ms (로컬, 전후 각 20회)
- AI 추천이 실패하면 다른 모델, 그다음 점수 계산으로 넘어가게 해 둬서, 발표 이틀 전 사용량 한도가 바닥났을 때도 추천은 결과가 나왔습니다
- 석 달 뒤 EC2에 Docker Compose로 직접 배포했고, 막힌 네 군데를 [배포 문서](https://github.com/luster-woo/finance_pjt/tree/master/deploy)에 정리했습니다. 지금은 인스턴스를 내려 접속 주소는 없습니다

### SSabway · 지하철 실내 길안내와 화상 상담

<img src="https://github.com/luster-woo/SSabway/raw/main/assets/%EC%98%AC%EB%A6%B4%EC%82%AC%EC%A7%84_SSabway/thumb-admin-consult.png" width="480" alt="SSabway 관리자 앱 화상 상담">

역 안 표지판을 찍으면 길을 알려 주고, 필요하면 역무원과 화상으로 연결해 주는 서비스입니다. 프론트엔드에서 관리자 앱을 전담했습니다.

- 휴대폰마다 화면 비율이 0.46~0.56으로 달라 상담원과 사용자가 서로 다른 화면을 보던 문제를, 접속할 때 실제 비율을 재서 주고받는 방식으로 팀원과 함께 고쳤습니다

### SOBI · 소상공인 정책자금 플랫폼

<img src="https://github.com/luster-woo/Sobi/raw/develop/docs/screenshots/%EC%98%AC%EB%A6%B4%EC%82%AC%EC%A7%84_Sobi/thumb-10_dashboard.png" width="480" alt="SOBI 대시보드">

소상공인에게 맞는 정책자금과 대출을 찾아 주고 신청 서류를 돕는 플랫폼입니다. 프론트엔드 파트장으로 인증, 대시보드, 마이페이지, 프론트 보안을 맡았습니다.

- 첫날 올린 기반 위에 MR 하나로 파일 96개가 들어와 일정이 이틀 밀렸습니다. 그 뒤로 공통 구조, 공용 UI, 기능 순서로 나눠 올리고 MR 전에 화면을 같이 띄워 보기로 했고, 되돌린 병합은 더 없었습니다
- Claude가 토큰을 `localStorage`에 넣는 코드를 제안한 걸 보안 점검 중에 발견해 빼고, ESLint 규칙으로 다시 못 들어오게 막았습니다

[자세히 보기](https://github.com/luster-woo/Sobi/blob/develop/PORTFOLIO.md)

## 기술

| | |
|---|---|
| 주로 씀 | Java, Spring Boot, JPA · Python, Django REST Framework · React, TypeScript · PostgreSQL, Redis, RabbitMQ |
| 해 봄 | Docker Compose, nginx, AWS EC2 배포(상시 운영 경험은 없음) · LLM API, RAG · JUnit, Mockito |
| 팀 환경에서 씀 | Jenkins, GitLab CI, Prometheus, Grafana (팀 인프라 담당이 구축) |
| 자격 | 정보처리기사 · SQLD · ADsP · 컴퓨터활용능력 1급 |

## 그 밖에

- [codetree](https://github.com/luster-woo/codetree) · 코드트리 585문제를 59일 동안 풀고 주제별로 정리
- [ssafy_gumi_study](https://github.com/luster-woo/ssafy_gumi_study) · 6명이 3.5개월 한 알고리즘 스터디, Fork와 PR로 제출하고 서로 리뷰
- [TIL](https://github.com/luster-woo/TIL) · SSAFY 1학기에 배운 것 정리
