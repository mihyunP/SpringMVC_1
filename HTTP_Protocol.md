# HTTP 프로토콜

### 1)  Web 기본 용어 정리

`웹 서버(Web Server)` : HTTP 기반으로 동작하며 클라이언트의 요청에 따라 **정적 리소스(html, css, js, 이미지, 영상 등)**를 클라이언트에게 제공해주는 주체

예)NGINX, APACHE

cf. `웹 애플리케이션 서버(Web Application Server)` : HTTP 기반으로 동작하며 웹서버 기능 + 프로그램 코드를 실행해서 **애플리케이션 로직** 수행하여 동적 html(사람들마다 다른 html 페이지 보여줄 수 있음), http API(JSON), 서블릿, JSP, 스프링 MVC 제공

예) 톰캣, 제티, Undertow

`웹 클라이언트(Web Client)` : 필요한 데이터를 웹 서버에 요청하는 주체

`웹 브라우저(Web Browser)` : Request Message를 작성하여 웹 서버에 전달하고, 웹 서버로부터 전달받은 Response Message를 해석하여 사용자에게 보여주는 소프트웨어 Ex) Internet Explorer, Chrome, Edge, Safari, Firefox, Netscape Navigator 등

`URL(Uniform Resource Locator)` :  자원의 위치

Ex) [http://opentutorials.org:3000/mainVisit Website](http://opentutorials.org:3000/main) 

 ` URI(Uniform Resource Identifier)` : 자원의 식별자(pathVariable방식, QueryParameter 방식)

Ex) [http://opentutorials.org:3000/main?id=HTML&page=12Visit Website](http://opentutorials.org:3000/main?id=HTML&page=12)



![image](https://user-images.githubusercontent.com/69749222/189536720-4cfdf7d3-59af-4924-97e2-d2783cfbd0df.png)

![image](https://user-images.githubusercontent.com/69749222/189536738-1d44caea-e04f-49db-83b9-9d3634b450c2.png)


### 2) HTTP 프로토콜

![image](https://user-images.githubusercontent.com/69749222/189536689-2927e72d-3c8d-416c-9935-c4f38f8a7e36.png)

: HyperText Transfer Protocol, 

HTML문서, 이미지, 동영상, 오디오, 텍스트 문서 등 리소스들을 가져올 수 있도록 해주는 전송 프로토콜(cf. URI : 자원의 위치를 알려주기 위한 프로토콜) 

웹 상에서 클라이이언트(브라우저)-서버 간에 정보(데이터)를 주고받을 수 있는 프로토콜

클라이언트-서버 모델을 따르는 프로토콜

애플리케이션 레벨의 프로토콜로 TCP/IP위에서 작동

Connectionless 방식 / stateless 방식(서버와 계속 세션을 맺고 있는게 아니라 원하는 정보를 받으면 세션 종료)



### 3) HTTP 메시지

: 서버(Server)와 클라이언트(Client)가 HTTP 통신을 할 때 주고받는 메시지,

- **Request Message** == 클라이언트가 서버에게 자료를 요청하는 메시지, 클라이언트(브라우저)가 생성
- **Response Message** == 서버가 클라이언트에게 요청에 대한 응답 메시지, 서버가 생성



**HTTP Request Message**

: 클라이언트(브라우저) -> 서버 전송하는 메시지

-Request 메시지 포맷-

![image](https://user-images.githubusercontent.com/69749222/189536773-1b21df22-39c2-4e54-9c61-7d6eda88174b.png)

-Request 메시지 예시-

![image](https://user-images.githubusercontent.com/69749222/189536796-f2e5d401-d0e5-4587-9e23-28bec46b4fa9.png)

`요청 라인(Request Line)`, `요청 헤더(Request Header)`, `공백 라인(Blank Line)`, `요청 바디(Request Body)`로 구성

```
① 요청 라인: 리퀘스트 메소드 / 리퀘스트 URI / HTTP 버전
② 요청 헤더: Host, Accept, User-Agent, Cokie, Referer 등

Host: 클라이언트가 요청한 도메인 정보
Connection: Request 후 연결을 닫을 것인지 유지할 것인지를 나타냄 Ex) Close / Keep-Alive
User-Agent: 사용자 웹 브라우저 종류 및 버전 정보
Accept: 웹 서버로부터 수신되는 데이터 중 웹 브라우저가 처리할 수 있는 데이터의 형식 정의, MIME  
Ex) text, html 형태의 문서를 처리할 수 있고, `*/*`는 모든 문서를 처리할 수 있다는 의미
Accept-Encoding: 클라이언트가 지원하는 Encoding 타입을 열거함 Ex) gzip, deflate 등
Accept-Language: 클라이언트가 다룰 수 있고 선호하는 언어 타입이 열거
Accept-Charset: 클라이언트가 다룰 수 있고 선호하는 문자 집합이 열거 Ex) UTF8, BIG5, ISO-8859-2 등
Content-Length: POST Request를 사용할 때, Request Body의 데이터 길이
Content-Type: POST Request를 사용할 때, Request Body 데이터의 형식을 MIME 타입으로 나타냄
Cookie: 클라이언트 로컬에 저장되는 key-value쌍의 데이터 파일
Referer: 경유한 웹 사이트에 대한 정보

③ 공백 라인: 요청 헤더와 요청 바디를 구분하는 라인
④ 요청 바디: 클라이언트가 서버에 실제 요청한 내용
```

---------

**HTTP Response Message**

: 서버 -> 클라이언트(브라우저) 전송하는 메시지

-Respoonse 메시지 포맷-

![image](https://user-images.githubusercontent.com/69749222/189536816-a9cf11cf-3b06-41b0-aa58-bfc05e872ab5.png)
-Respoonse 메시지 예시-

![image](https://user-images.githubusercontent.com/69749222/189536879-df323249-d090-4170-9e17-e980072479b1.png)

브라우저는 응답 메시지를 수신하고 해석한 후에 브라우저 창에 메시지 내용을 표시함,
응답 메시지는 크게 `상태 라인(Status Line)`, `응답 헤더(Response Headers)`, `공백 라인(A blank line)`, `응답 바디(Requset Message Body)`로 나뉜다.

```
① 상태 라인: HTTP 버전, 상태 코드, Reason_Phrase
② 응답 헤더: Date, Server, Content-Type, Last-Modified 등

Server: Request 처리를 위한 서버의 소프트웨어 정보
Content-Type: 컨텐츠의 미디어 타입을 알려주는데 사용된다. Ex) Content-Type: text/html; charset=ISO-8859-4
Content-Encoding: Body에 포함된 컨텐츠의 인코딩 형태를 알려주는데 사용된다. ex) Content-Encoding: gzip
Last-Modified: 리소스가 마지막으로 업데이트되었다고 여겨지는 date/time을 제공하는데 사용된다. 
Ex) Last-Modified: Thu, 15 Oct 2020 14:47:59 GMT
WWW-Authenticate: Request-URI에 적용될 수 있는 인증체계와 매개변수 정보
Allow: Request-URI에서 지원하는 Method
Content-Language: 컨텐츠에서 사용된 언어를 나타내는데 사용된다.
Content-Location: 메시지에 포함된 리소스의 위치를 공유하는데 사용된다.
Content-MD5: Body 컨텐츠의 MD5 코드를 제공하는데 사용된다.

③ 공백 라인: 요청 헤더와 요청 바디를 구분하는 라인
④ 응답 바디: 실제 응답받은 메시지(데이터)
```



### 4) HTTP Request 메소드

 : 클라이언트가 웹 서버에게 사용자 요청의 목적이나 종류를 알리는 수단

![image](https://user-images.githubusercontent.com/69749222/189536894-7921fcff-15cd-44bd-a7c8-2d4b8cfbac06.png)

(주요 메소드 5가지)

- GET : 리소스 조회
- POST : 요청 데이터 처리, 주로 데이터 등록에 사용
- PUT : 리소스를 대체, 해당 리소스가 없으면 생성
- PATCH : 리소스를 일부만 변경
- DELETE : 리소스 삭제

(기타 메소드 4가지)

- HEAD: GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS: 대상 리소스에 대한 통신 가능 옵션을 설명(주로 CORS에서 사용)
- CONNECT: 대상 자원으로 식별되는 서버에 대한 터널을 설정
- TRACE: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행



### 5)HTTP Response 코드

Status Code는 3자리 숫자 코드로 Request에 대한 응답으로 서버에서 생성함

- **1xx (Informational)**: 요청이 수신되어 처리중

- **2xx (Successful)**: 요청 정상 처리

```
200 OK : 요청 성공
201 Created : 요청 성공해서 새로운 리소스가 생성됨
202 Accepted : 요청이 접수되었으나 처리가 완료되지 않았음
204 No Content : 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음
```

- **3xx (Redirection)**: 요청을 완료하려면 추가 행동이 필요, 리다이렉트

```
301 Moved Permanently : 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음
302 Found : 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음
303 See Other : 리다이렉트시 요청 메서드가 GET으로 변경
304 Not Modified : 캐시를 목적으로 사용
307 Temporary Redirect : 리다이렉트시 요청 메서드와 본문 유지(요청 메서드를 변경하면 안된다.)
308 Permanent Redirect : 리다이렉트시 요청 메서드와 본문 유지(처음 POST를 보내면 리다이렉트도 POST 유지)
```

- **4xx (Client Error)**: 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음

```
400 Bad Request : 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음
401 Unauthorized : 클라이언트가 해당 리소스에 대한 인증이 필요함
403 Forbidden : 서버가 요청을 이해했지만 승인을 거부함
404 Not Found : 요청 리소스를 찾을 수 없음
```

- **5xx (Server Error)**: 서버 오류, 서버가 정상 요청을 처리하지 못함

```
500 Internal Server Error : 서버 문제로 오류 발생, 애매하면 500 오류\
503 Service Unavailable : 서비스 이용 불가
```
