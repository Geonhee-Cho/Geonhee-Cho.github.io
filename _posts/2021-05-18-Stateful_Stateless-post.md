---
title: "Stateful Service vs Stateless Service"
date: 2021-05-18 16:18:28 -0400
categories: study
---

Stateful Service vs Stateless Service

Stateful Service
1. 클라이언트의 세션 정보를 server에 저장
2. 세션 'State(상태)'에 따른 응답

Stateless Service
1. 클라이언트의 세션 정보를 server에 저장하지 않음
2. 세션 'State(상태)'에 무관한 응답

HTTP와 REST 모두 Stateless한 성격을 가진 녀석들이며,
HTTP는 Statelss한 성격을 가진 '프로토콜'
REST는  Stateless한 성격을 가진 '설계 구조'

scale out 시 Stateful 서비스의 경우, client의 세션 정보가 새로 scale out된 서버에 저장 되어 있지 않다.
따라서 세션 정보를 옮겨주는 등의 부수적인 관리가 필요하다.
하지만 Stateless 서비스의 경우, server는 client 세션 관리를 하지 않으므로 추가적인 작업이 필요 없다

* Scale Up : 
서버 자체의 Spec 을 향상시킴으로써 성능을 향상시킨다.
Vertical Scaling 이라 불리기도 한다.
서버 자체의 갱신이 빈번하여 정합성 유지가 어려운 경우(주로 OLTP 를 처리하는 RDB 서버의 경우) Scale Up 이 효과적이다.
성능 향상에 한계가 있으며 성능 증가에 따른 비용부담이 크다.(대신 관리 비용이나 운영 이슈가 Scale Out 에 비해 적어 난이도는 쉬운 편)
대신 서버 한대가 부담하는 양이 많기 때문에 다양한 이유로 서버에 문제가 생길 경우 큰 타격이 불가피하다.

* Scale Out :
서버의 대수를 늘려 동시 처리 능력을 향상시킨다.
Horizon Scaling 으로 불린다.
단순한 처리의 동시 수행에 있어 Load 처리가 버거운 경우 적합하다.
API 서버나, 읽기 전용 Database, 정합성 관리가 어렵지않은 Database Engine 등에 적합하다.
스케일 아웃은 일반적으로 저렴한 서버 여러 대를 사용하므로 가격에 비해 뛰어난 확장성 덕분에 효율이 좋지만 대수가 늘어날 수록 관리가 힘들어지는 부분이 있고, 아키텍처의 설계 단계에서부터 고려되어야 할 필요가 있다.

---

laravel 프레임 워크를 이용하여 간단한 토이 프로젝트 개발중 사용하였던 route 파일을 web과 api로 분리하는 도중 발생한 문제 해결을 위해 간단히 정리하였습니다.

laravel의 route는 web.php, api.php, console.php 로 구성되어 있고, 각각 web, api, artisan명령어를 담당하고 있습니다.

이 때 api.php는 stateless 상태이기 때문에 미들웨어에서 state를 인증하기 위해서는 추가적인 코드가 필요합니다.

저는 session으로만 로그인을 구현하였기 때문에 api.php에서 로그인 체크 middleware를 사용 시 에러가 발생하였습니다.

현재 프로젝트는 laravel을 익혀보기위해 간단하게 개발중이지만 다음 토이프로젝트를 진행 할 때는 로그인에 더욱 신경 써 개발해야 할 것 같습니다..

다음은 oauth 2.0 에 대해 공부하겠습니다.

감사합니다.
