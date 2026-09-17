# 이윤우

백엔드 개발자를 준비하고 있습니다.
경북대학교 컴퓨터학부 글로벌소프트웨어융합전공(복수전공), SSAFY 15기입니다.

생명과학을 전공하다 복수전공으로 개발을 시작했습니다. 금융상품 추천 서비스 FinFit의 백엔드를 맡아 만들었고, 프로젝트가 끝난 뒤 AWS EC2에 직접 배포했습니다. 외부 API가 느려지거나 멈추는 상황을 겪으면서, 의존하는 서비스가 실패해도 전체가 멈추지 않게 만드는 데 관심을 두고 있습니다.

- Email: leeyw001013@naver.com
- 자격: 정보처리기사, SQLD, ADsP, 컴퓨터활용능력 1급
- 알고리즘: [solved.ac](https://solved.ac/profile/leeyw1709) · 코드트리 585문제

<br>

## Projects

### [FinFit](https://github.com/luster-woo/finance_pjt) · 금융성향 기반 금융상품 추천 서비스

`2026.05~06` `2인` `백엔드 담당` `Python` `Django REST Framework` `SimpleJWT` `Gemini`

금융성향 검사 결과에 맞춰 예·적금, 주식, 카드를 추천하고 AI 상담을 제공하는 서비스입니다. 인증부터 추천, AI 상담까지 API를 설계·구현하고 외부 API 5종을 연동했습니다.

- 사용자가 상품을 볼 때마다 FinLife API(응답 4~5초)를 부르던 구조를, 관리자 API로 DB에 미리 저장하고 ORM으로 조회하도록 바꿔 **상품 조회를 1초 이내로 줄였습니다.**
- 발표 이틀 전 SSAFY GMS가 멈췄을 때 원인을 바로 좁히고, **Gemini 1.5 Flash를 대체 경로로 붙여** 외부 API 하나가 멈춰도 서비스 전체 오류로 번지지 않게 했습니다.
- AI 추천이 매번 달라져 금리 40, 수익 절대액 30, 상품 유형 15, 은행 신뢰도 15의 **평가 기준을 직접 정해** 프롬프트에 넣었습니다. 금리만 보면 실제 이자가 적은 상품이 위로 올라와, 금리와 만기 예상 이자를 따로 나눴습니다.
- 로그아웃 후에도 서버 토큰이 유효하게 남는 문제를 SimpleJWT Token Blacklist로 막았습니다.

**운영 배포 (2026.09)**

프로젝트 기간 안에는 배포하지 못했습니다. 완성 기준을 로컬 실행으로 좁게 잡은 탓이라 판단했고, 3개월 뒤 다시 돌아가 AWS EC2에 배포했습니다.

- nginx, Django·gunicorn, PostgreSQL 16, 스케줄러 전용 컨테이너 4개를 Docker Compose로 구성했습니다.
- 서버에 올리기 전에 운영 구성을 로컬에서 먼저 실행해 봤고, 서버에서는 애플리케이션 오류 없이 **인프라 문제 4건만** 해결했습니다.
  - 외부 접속 불가: localhost, 포트 바인딩, OS 방화벽을 차례로 확인한 뒤 보안 그룹 인바운드 누락을 찾았습니다.
  - 디스크 부족: 기본 8GiB EBS를 스왑 파일이 차지하고 있어, 볼륨을 20GiB로 늘리고 파티션을 확장했습니다.
- 절차와 장애 기록은 [deploy](https://github.com/luster-woo/finance_pjt/tree/master/deploy) 폴더에 남겼습니다. 검증 후 인스턴스를 종료해 지금은 접속 주소가 없고, HTTPS는 적용하지 않았습니다.

<br>

### [SSabway](https://github.com/luster-woo/SSabway) · AI 표지판 인식 기반 지하철 실내 길안내·화상 상담

`2026.07~08` `6인` `프론트엔드 담당` `React 19` `TypeScript` `OpenVidu` `MSW` `SSAFY 공통 프로젝트 우수상(2위)`

역 안의 표지판을 촬영하면 위치를 인식해 길을 안내하고, 필요하면 상담원과 화상으로 연결하는 서비스입니다. 사용자·관리자 화면 17개와 화상 상담, 4개국어 적용을 맡았습니다. 백엔드, AI 모델, CI/CD는 다른 팀원이 담당했습니다.

- 기기마다 화면 비율(0.46~0.56)이 달라 상담원과 사용자가 다른 영역을 보던 문제를, 각 브라우저가 비율을 직접 재서 OpenVidu 시그널로 주고받는 방식으로 해결했습니다.
- 백엔드 API가 3일 늦어졌을 때 MSW 도입을 제안해, API를 기다리지 않고 담당 화면 17개를 먼저 개발했습니다.
- 한·영·일·중 4개국어를 전 화면에 적용했습니다.

<br>

## Tech

| 분야 | 사용한 기술 |
|---|---|
| Backend | Python, Django, Django REST Framework, SQL |
| Frontend | React, TypeScript, Vue.js, Zustand, TanStack Query |
| 배포 | Docker Compose, nginx, gunicorn, PostgreSQL, AWS EC2 |
| 협업 | Git, GitLab MR, Git Flow |

<br>

## Repositories

| 저장소 | 내용 |
|---|---|
| [finance_pjt](https://github.com/luster-woo/finance_pjt) | FinFit 소스와 배포 구성·기록 |
| [SSabway](https://github.com/luster-woo/SSabway) | SSabway 소스 |
| [codetree](https://github.com/luster-woo/codetree) | 코드트리 585문제(59일) 풀이를 주제별로 정리 |
| [ssafy_gumi_study](https://github.com/luster-woo/ssafy_gumi_study) | 6명이 3.5개월 진행한 알고리즘 스터디. Fork & PR 제출, 상호 코드 리뷰 |
| [ssafy-pjt](https://github.com/luster-woo/ssafy-pjt) | SSAFY 관통 프로젝트 정리 |
| [TIL](https://github.com/luster-woo/TIL) | SSAFY 1학기 학습 기록 |
