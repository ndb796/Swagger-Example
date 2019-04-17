## Swagger
### Swagger와 Open API의 개념
* [블로그 자료](https://ndb796.tistory.com/249)
* Swagger는 특정한 프로그램에 존재하는 API 기능을 명세하고, API 기능을 바로 테스트할 수 있도록 하는 도구.
* 프로젝트에 참여하는 개발자가 많으면 서버 개발자와 클라이언트 개발자의 소통을 위해 API 명세는 반드시 필요.
* 특히 모바일 개발에 있어서 더 사용 빈도가 높음. API를 명세하는 작업은 매우 귀찮고, 번거로운 작업이 될 수 있음.
* 따라서 API 명세와 테스트를 한 번에 쉽고 빠르게 하도록 도와주는 Swagger를 이용하면 효과적.
* 한 번 써보면, 팀 프로젝트가 아닌 개인 프로젝트에서도 이용하게 될 정도로 유용함.
* API를 이용함에 있어서 보안 설정, 다양한 부가적인 관리 기능을 넣을 수 있음.
* 그래서 현재 우리 개발 팀에서도 API 명세 도구로 Swagger를 채택하여 사용하고 있음.
* Swagger는 기본적으로 REST API를 채택하며, 마이크로서비스 아키텍처와 맥락을 같이함.
* [Open API](https://github.com/OAI/OpenAPI-Specification)란? REST API를 위한 표준 API 명세 규격을 의미함.
* API에 대한 요청(Request), 응답(Response), API 접근 경로를 포함한 전체 API 명세 방법을 규정함.
* 2019년 현재 최신 버전은 OpenAPI 3.0.0 버전이며 Swagger는 OpenAPI 3.0.0을 지원함.
* OpenAPI는 YAML 혹은 JSON 형식을 지원함. Swagger는 YAML 형식을 권장함.
* [Swagger Hub](https://swagger.io/tools/swaggerhub/) 접속 및 로그인.
* Swagger를 이용하는 방법은 일반적으로 두 가지임.
1) 특정 서버 프로그래밍 언어를 이용해 Swagger API를 종속적으로 이용하는 방식. (흔히 Spring에서 어노테이션을 붙여서 API 명세함.)
2) 서버 프로그래밍 언어를 거치지 않고 Swagger API를 독립적으로 이용하는 방식. (yaml 파일을 작성하여 API를 명세함.)
* [Create New] - [Create New API] - [OpenAPI Version 3.0.0] - [Petstore] - Petstore 이름으로 생성.
* Petstore 예제 확인 가능. 본 예제는 Swagger API를 독립적으로 이용하는 방식.
* 왼쪽에는 API 명세서의 요약, 중간에는 Swagger Editor, 오른쪽에는 API 명세서 전체 내용(Swagger UI)이 출력됨.
* yaml이라는 데이터 양식을 이용해 API를 명세할 수 있음.
* 이제 대충 어떻게 생겼는지 이해할 수 있음.
* 구체적인 내용을 공부하고자 한다면 [Swagger Tutorial](https://app.swaggerhub.com/help)로 이동.
### 간단한 REST API 명세해보기
* [Create New] - [Create New API] - [OpenAPI Version 3.0.0] - Template: [none] - Name: [Google_API_Test] - Version: [1.0.0] - Title: [Google_API_Test] - Description: [Google_API_Test]
* 구글 자동완성 API 테스트
```
openapi: 3.0.0
info:
  version: '1.0.0'
  title: 'UserAPI'
  description: 'UserAPI'
servers:
  - description: SwaggerHub API Auto Mocking
    url: https://virtserver.swaggerhub.com/ndb796/UserAPI/1.0.0
  - description: Google API
    url: https://www.google.com/
  - description: JSON Placeholder API
    url: https://jsonplaceholder.typicode.com/
paths:
  /todos/{userId}:
    get:
      summary: Returns a user by ID
      parameters:
        - name: userId
          in: path
          required: true
          description: The ID of the user to return
          schema:
            type: integer
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                type: object
                properties:
                  userId:
                    type: integer
                  id:
                    type: integer
                  title:
                    type: string
                  completed:
                    type: boolean
  /complete/search:
    get:
      summary: 자동완성 검색 결과를 반환합니다.
      parameters:
        - name: q
          in: query
          schema:
            type: string
        - name: client
          in: query
          schema:
            type: string
      responses:
        '200':
          description: A Text File
          content:
            text/plain:
              schema:
                type: string
```
* Swagger Hub가 제공하는 프록시 기능을 통해 결과 확인 가능
2) https://jsonplaceholder.typicode.com/todos/1
1) https://www.google.com/complete/search?q=asd&client=psy-ab
* Mocking은 API를 테스트하기 위해 가짜 값을 이용하는 것을 의미.
### 웹 문서용 Swagger UI 사용해보기
* Swagger UI 웹 문서 버전을 사용하면 독립적인 Swagger UI를 이용할 수 있음.
* [Swagger UI](https://github.com/swagger-api/swagger-ui)에 접속.
* [Download Zip] - 압축 풀기 - [dist] 폴더로 완성된 형태의 Swagger UI 이용 가능.
* [dist] 폴더 빼고 나머지 폴더 삭제해도 됨.
* 원하는 Swagger 프로젝트 [Export] - [Download API] - [YAML Resolved] - 압축 풀기 - openapi.yaml 파일을 [dist] 폴더에 붙여넣기.
* 웹 문서용 Swagger UI를 위해서는 웹 서버에 YAML 파일이 올라가 있어야 함.
* [dist] 폴더의 위치로 이동 및 웹 서버 구동 테스트.
```
npm install -g http-server
http-server --cors
```
* http://localhost:8080/ 접속 이후에 Swagger UI 동작 확인. 
* [dist] 폴더 내부의 index.html 수정 - url 경로를 "http://localhost:8080/openapi.yaml"로 수정.
* http://localhost:8080/ 접속 이후에 Swagger UI 동작 재확인. 
### 설치형 Swagger UI 사용 및 API Key 설정해보기
* [블로그 자료](https://ndb796.tistory.com/253)
* Swagger UI를 서버 프로그램과 함께 설치하여 사용할 수 있음. (종속적인 방법)
* 한 번 정의된 내용은 바꾸기 힘들지만, 익숙해지면 개발 속도가 매우 빠름.
* Swagger라는 패키지를 이용하면 Swagger 프로젝트를 빠르게 만들어서 개발할 수 있음.
* 필자는 별로 선호하지는 않음. 근데, 상당수 프로젝트가 이런 형식을 이용하고 있음. 특히 Spring.
```
# 윈도우 기준
npm install -g swagger
# 특정 폴더로 이동하기
cd C:\Study
swagger project create swagger
# [Express] 프로젝트 설정하기
cd swagger
swagger project start
# http://localhost:10010/hello?name=Scott 접속하여 기본적으로 만들어진 API 테스트
```
* app.js를 수정하여 Swagger UI 추가하기
```
# swagger-ui 라이브러리를 app에 추가합니다.
var SwaggerUi = require('swagger-tools/middleware/swagger-ui');

SwaggerExpress.create(config, function(err, swaggerExpress) {
  ...
  swaggerExpress.runner.swagger.host = '127.0.0.1:10010';
  app.use(SwaggerUi(swaggerExpress.runner.swagger));
  swaggerExpress.register(app);
  ...
});
```
* /docs 경로에 들어가 Swagger UI를 확인하기
* Swagger UI에 API Key 설정하는 방법
```
# app.js 파일 수정하기
# API Key 설정 내용을 추가합니다.
var config = {
  appRoot: __dirname, // required config
  swaggerSecurityHandlers: {
    api_key: function (req, authOrSecDef, scopesOrApiKey, cb) {
      // 요청 헤더값이 api_key 이고 값이 'my_key'일 경우에만 실행을 허용한다.
      if ('my_key' === scopesOrApiKey) {
        cb();
      } else {
        cb(new Error('access denied!'));
      }
    }
  }
};
# api/swagger/swagger.yaml 파일 수정하기
# 'definitions'라고 쓰인 코드 위에 넣습니다.
securityDefinitions:
  api_key:
    type: apiKey
    in: query
    name: api_key
security:
  - api_key: [  ]
```
* API Key를 입력하여 Swagger UI가 구동되는지 테스트
* API 내용을 변경하고 싶다면 어떻게 하면 될까?
```
# api/controllers/hello_world.js 파일에 API 추가하기
function adder(req, res) {
  let one = req.query.one;
  let two = req.query.two;
  let result = Number(one) + Number(two);
  res.json(String(result));
}
# api/controllers/hello_world.js 파일의 module.exports
module.exports = {
  hello: hello,
  adder: adder
};
# api/swagger/swagger.yaml 파일에 API 추가하기
  /adder:
    x-swagger-router-controller: hello_world
    get:
      description: Adder API
      operationId: adder
      parameters:
        - name: one
          in: query
          description: First Value
          required: true
          type: integer
        - name: two
          in: query
          description: Second Value
          required: true
          type: integer
      responses:
        "200":
          description: Success
          schema:
            $ref: "#/definitions/AdderResponse"
        default:
          description: Error
          schema:
            $ref: "#/definitions/ErrorResponse"
# api/swagger/swagger.yaml 파일의 definitions에 추가하기
  AdderResponse:
    required:
      - result
    properties:
      result:
        type: integer
```
* module.exports에 함수명을 넣어야, 실제로 API 형태로서 서버가 동작함.
* operationId는 실제로 존재하는, export 된 함수를 가리킬 수 있도록 해야 동작함.
### 간단한 API 기능 구현해보기
* 독립형으로 Swagger를 돌려 보기
* Express를 이용해 간단한 API 구현하기
```
# 새로운 Express 프로젝트 만들어 보기
cd C:\Study\Server API
npm init
# (Enter) 이후 프로젝트 생성 완료
# 프로젝트 폴더에 app.js 파일 생성 및 작성하기
var express = require('express');
var app = express();

app.get('/', function (req, res) {
  res.send('Hello World!');
});

app.listen(3000, function () {
  console.log('Server listening on port 3000!');
});
# 작성된 서버 프로그램 구동하기
npm install --save express
node app.js
# 사용자 이름에 유니코드 있을 때 오류 발생 가능
```
* 더하기 API 작성해보기
```
app.get('/adder', function (req, res) {
  let one = req.query.one;
  let two = req.query.two;
  let result = Number(one) + Number(two);
  res.send(String(result));
});
```
* http://localhost:3000/adder?one=1&two=2 테스트
* 정적 파일 제공하는 방법 알아보기
```
# app.js 파일에 코드 추가하기
app.use(express.static('swagger_ui'));
# 루트 폴더에 swagger_ui 폴더 생성하기
# swagger_ui 폴더 안에 test.html 파일 생성하기
Hello World
```
* http://localhost:3000/test.html 테스트
### 나의 API에 독립형 Swagger UI 달아보기
* [Swagger UI](https://github.com/swagger-api/swagger-ui)에 접속.
* [Download Zip] - 압축 풀기 - [dist] 폴더로 완성된 형태의 Swagger UI 이용 가능.
* [dist] 폴더 빼고 나머지 폴더 삭제해도 됨.
