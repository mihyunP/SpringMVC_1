# 섹션 1. 웹 애플리케이션 이해

### 웹 서버, 웹 애플리케이션 서버

웹 - HTTP 기반



HTTP 메시지에 모든 것을 전송

: HTML, TEXT • IMAGE, 음성, 영상, 파일 • JSON, XML (API)등 거의 모든 형태의 데이터 전송 가능, 서버간의 데이터 주고받기 가능



웹서버 vs 웹애플리케이션서버(WAS)

**웹서버**

: HTTP 기반으로 동작, 

`정적 리소스`(html, css, js, 이미지, 영상 등) 제공

예)NGINX, APACHE

![image-20220828152919764](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828152919764.png)



**웹애플리케이션서버(WAS)**

: HTTP 기반으로 동작, 

웹서버 기능 + 프로그램 코드를 실행해서 `애플리케이션 로직` 수행

동적 html(사람들마다 다른 html 페이지 보여줄 수 있음), http API(JSON), 서블릿, JSP, 스프링 MVC

예) 톰캣, 제티, Undertow

![image-20220828153220132](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828153220132.png)



웹 시스템 구성 - WAS, DB 필수

*WAS는 정적 리소스, 애플리케이션 로직 모두 제공 가능

WAS가 너무 많은 역할을 담당하면 서버 과부하 우려가 있음, 

가장 비싼 애플리케이션 로직이 정적 리소스 때문에 수행이 어려울 수 있고, WAS 장애 시 오류 화면도 노출 불가능함

웹 시스템 구성 - WEB, WAS, DB

![image-20220828153702612](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828153702612.png)

-> Web Server를 추가하여 정적 리소스는 웹 서버가 처리, WAS는 애플리케이션 로직 전담



### 서블릿

html form 데이터 전송

![image-20220828154205923](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828154205923.png)



서버에서 처리해야 하는 업무

![image-20220828154458088](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828154458088.png)

비즈니스 로직 제외 모든 웹 애플리케이션 서버의 역할을 서블릿이 대신해준다!

서블릿

![image-20220828154649151](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828154649151.png)

urlPatterns(/hello)의 URL이 호출되면 서블릿 코드가 실행

HTTP 요청 정보를 편리하게 사용할 수 있는 HttpServletRequest

HTTP 응답 정보를 편리하게 사용할 수 있는 HttpServletResponse

=> 개발자는  HTTP 스펙을  편리하게 사용할 수 있음



서블릿 HTTP 요청, 응답 흐름

![image-20220828155000336](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828155000336.png)

HTTP 요청 시,

1) WAS는 Request, Response 객체를 새로 만들어서 서블릿 객체 호출
2) 개발자는 Request 객체에서 HTTP 요청 정보를 편리하게 꺼내서 사용
3) 개발자는 Response 객체에서  HTTP 응답 정보를 편리하게 입력
4) WAS는 Response 객체에 담겨있는 내용으로 HTTP 응답 정보를 생성



서블릿 컨테이너

톰캣처럼 서블릿을 지원하는 WAS를 서블릿 컨테이너라고 함

서블릿 객체를 생성, 초기화, 호츨,종료하는 생명주기 관리

서블릿 객체는 싱글톤으로 관리

Request, Reponse 객체는 http 요청별로 새로 생성되지만, 서블릿 객체는 최초 로딩 시점에 서블릿 객체 미리 만들어놓고 재활용 모든 고객 요청은 동일한 서블릿 객체 인스턴스에 접근, 서블릿 컨테이너 종료시 함께 종료



### 동시요청 - 멀티 쓰레드

![image-20220828160319407](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828160319407.png)

쓰레드가 서블릿 호출함

쓰레드 : 애플리케이션 코드를 하나하나 순차적으로 실행함

자바 메인 메서드를 처음 실행하면 main이라는 이름의 쓰레드가 실행

![image-20220828160528137](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828160528137.png)

![image-20220828160603064](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828160603064.png)

요청이 올때마다 쓰레드 생성



![image-20220828161038024](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828161038024.png)

![image-20220828161203766](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828161203766.png)

쓰레드 풀

특징

요청마다 쓰래드 생성의 단점 보완

필요한 쓰레드를 쓰레드 풀에 보관하고 관리한다

쓰레드 풀에 생성 가능한 쓰레드의 최대치를 관리한다. 톰캣은 최대 200개 기본 설정

사용

쓰레드가 필요하면 이미 생성되어있는 쓰레드를 쓰레드 풀에서 꺼내서 사용한다

사용을 종료하면 쓰레드 풀에 해당 쓰레드를 반납한다

최대 쓰레드가 모두 사용중이어서 쓰레드 풀에 쓰레드가 없을 때, 기다리는 요청을 거절하거나 특정 숫자만큼만 대기하도록 설정할 수 있다.

장점

쓰레드 생성 비용(CPU) 절약, 빠른 응답 시간



쓰레드 풀 너무 낮게 설정하면,

동시 요청 많으면, 서버 리소스는 여유롭자만 클라이언트 응답 지연

쓰레드 풀 너무 높게 설정하면,



멀티 쓰레드에 대한 부분은 WAS가 처리



### HTML, HTTP API, SSR, CSR

![image-20220828162530052](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828162530052.png)

![image-20220828162559011](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828162559011.png)

![image-20220828162630817](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828162630817.png)

![image-20220828162933498](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828162933498.png)

 주로 JSON 형태로 데이터 통신

UI 클라이언트 접점

앱 클라이언트(아이폰, 안드로이드, PC 앱)

웹 브라우저에서 자바스크립트를 통한 HTTP API 호출

React, Vue.js같은 웹 클라이언트



=> 정적 리소스, 동적 HTML, HTTP API

HTTP 방식으로 통신하는 3가지



SSR-서버 사이드 렌더링

: 서버에서 최종 HTML을 생성해서 클라이언트에 전달

주로 정적인 화면에 사용

관련기술 :  JSP, 타임리프 -> 백엔드 개발자

![image-20220828163413373](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828163413373.png)



CSR-클라이언트 사이드 렌더링

: HTML 결과를 자바스크립트를 사용해 웹 브라우저에서 동적으로 생성해서 적용

주로 동적인 화면에 사용, 웹 환경을 마치 앱에서 필요한 부분부분 변경할 수 있음

관련기술: React, Vue.js -> 프론트엔드 개발자

![image-20220828163653718](C:\Users\woori\AppData\Roaming\Typora\typora-user-images\image-20220828163653718.png)



### 자바 백엔드 웹 기술 역사

자바 웹 기술 역사

서블릿 -> JSP -> 서블릿+JSP=MVC패턴 -> MVC춘추전국시대(스트럿츠,웹워크,스프링MVC) -> 애노테이션 기반의 스프링 MVC -> 스프링 부트

*스프링 부트 : 스프링을 편리하게 사용할 수 있게해주는 껍데기, 스프링 부트는 서버를 내장하기 때문에 WAS 설치 불필요 -> 빌드 배포의 단순화

Web Servlet - Spring MVC

Web Reactive - Spring WebFlux

 

자바 뷰 템플릿 역사

JSP -> 프리마커, 벨로시티 -> 타임리프

