## Swagger
### 개요
* 특정한 프로그램에 존재하는 API 기능을 명세하고, API 기능을 바로 테스트할 수 있도록 함. 모바일 개발에 있어서 더 사용 빈도가 높음.
* 프로젝트에 참여하는 개발자가 많으면 서버 개발자와 클라이언트 개발자의 소통을 위해 API 명세는 반드시 필요.
* API를 명세하는 작업은 매우 귀찮고, 번거로운 작업이 될 수 있음.
* 따라서 API 명세와 테스트를 한 번에 쉽고 빠르게 하도록 도와주는 Swagger를 이용하면 효과적.
* 한 번 써보면, 팀 프로젝트가 아닌 개인 프로젝트에서도 이용하게 될 정도로 유용함.
* [Swagger Hub](https://swagger.io/tools/swaggerhub/) 접속 및 로그인.
* Swagger를 이용하는 방법은 일반적으로 두 가지임.
1) 특정 서버 프로그래밍 언어를 이용해 Swagger API를 종속적으로 이용하는 방식. (흔히 Spring에서 어노테이션을 붙여서 API 명세함.)
2) 서버 프로그래밍 언어를 거치지 않고 Swagger API를 독립적으로 이용하는 방식. (yaml 파일을 작성하여 API를 명세함.)
* [Create New] - [Create New API] - [OpenAPI Version 3.0.0] - [Petstore] - Petstore 이름으로 생성.
* Petstore 예제 확인 가능. 본 예제는 Swagger API를 독립적으로 이용하는 방식.
* 왼쪽에는 API 명세서의 요약, 중간에는 Swagger 코드, 오른쪽에는 API 명세서 전체 내용이 출력됨.
* yaml이라는 데이터 양식을 이용해 API를 명세할 수 있음.
* 이제 대충 어떻게 생겼는지 이해할 수 있음.
* 구체적인 내용을 공부하고자 한다면 [Swagger Tutorial](https://app.swaggerhub.com/help)로 이동.
