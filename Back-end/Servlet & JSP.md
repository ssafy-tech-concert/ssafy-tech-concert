<div align="center">
  <br />
  <h1>Servlet&JSP</h1>
  <br />
</div>

### 목차

1. [**Servlet&JSP**](#1)
2. [**WAS**](#2)

<br />

<div id="1"></div>

## Servlet & JSP

### Servlet

**웹 어플리케이션을 만들때 필요한 인터페이스**

웹 페이지등을 **동적**으로 생성, 데이터 처리를 수행하기 위해 자바로 작성된 프로그래밍

**형태**

- Java 코드 내에 HTML이 삽입되는 형태

### JSP

**형태**

- HTML 내에 Java가 삽입되는 형태

### MVC Pattern

- 스크립트 와 html을 작성하기 좋은 JSP를 보존하면서 서버 통신과 용이한 Servlet을 이용하여 고안된 디자인 패턴

![](https://images.velog.io/images/dgh03207/post/fe6a8776-3b92-4f7d-b45d-1bdeea97a740/KakaoTalk_20211013_050549894.png)

<div id="2"></div>

## WAS

**WebServer**

- HTTP 요청을 받아 정적인 컨텐츠들을 제공하는 컴퓨터 프로그램

* Apache란?

- 소프트웨어 단체 이름으로 **아파치 서버** 라는 것은 이 재단에서 후원하는 오픈소스 프로젝트 커뮤니티에서 만든 http 웹 서버를 말한다.

**WAS(Web Application Server)**

**Web Application**

- 웹에서 실행되는 응용 프로그램

  **Web Application Server**

- 인터넷 상에서 HTTP를 통해 사용자 컴퓨터나 장치에 애플리케이션을 수행해 주는 미들웨어(소프트웨어 엔진)
- 웹 어플리케이션을 실행시켜 필요한 기능을 수행하고 그 결과를 웹 서버에 전달
- 동적인 정보를 서비스하기 위해 필요한 서버
- Tomcat , Jeus , IBM WebSphere

![](https://images.velog.io/images/dgh03207/post/52f201e3-ad67-4a6e-9444-06c04c0a2c85/KakaoTalk_20211013_041308218.png)

1. Client가 WebServer에 HttpRequest를 보냄
2. 이것을 Web Server가 WebContainer에 위임함(웹서버와 소켓으로 통신)
3. WebContainer는 Servlet의 생명주기를 담당한다.
4. **멀티스레드**
   - Tomcat 서버가 다중 쓰레드를 생성,운영등 관리해주어 안정성에 대해 걱정하지 않아도 됨.
5. Servlet 인스턴스는 항상 1개만 존재->**Singleton Pattern**

**init() -> service()\_doGet(),doPost() -> destory()**

- init() 메소드
  - 한번만 수행
  - servlet 객체 초기화 역할을 수행한다.
- service(request,response)메소드
  - request타입에 따라 doGet,doPost()가 대표적으로 실행됨
  - 메소드가 return되면 해당 thread는 제거됨
- destroy()메소드
  - 한번만 수행됨
  - WAS가 갱신되거나 종료될 때 호출된다.
  - Servlet객체를 메모리에서 제거하는 역할을 수행함.

<br />
