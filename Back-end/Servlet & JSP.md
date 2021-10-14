<div align="center">
  <br />
  <h1> Servlet & JSP </h1>
  <br />
</div>



## 목차


1. [**Servlet&JSP**](#1)
2. [**WAS**](#2)

<br />


<div id="1"></div>

## Servlet & JSP

### Servlet

**웹 어플리케이션을 만들때 필요한 인터페이스**

웹 페이지등을 **동적**으로 생성, 데이터 처리를 수행하기 위해 자바로 작성된 프로그래밍

**형태**

* Java 코드 내에 HTML이 삽입되는 형태



### JSP

**형태**

* HTML 내에  Java가 삽입되는 형태

WAS에 의해 서블릿 클래스로 변환되어 사용되어 진다.



### MVC Pattern

![KakaoTalk_20211013_050549894](C:\Users\ayeong\Desktop\KakaoTalk_20211013_050549894.png)



<div id="2"></div>

## WAS



**WAS(Web Application Server)**

  **Web Application**

 - 웹에서 실행되는 응용 프로그램
 - HTML이 프로그래밍 언어가 아니기 때문에 있었던 한계를 극복가능해짐

  **Web Application Server**

- 웹 어플리케이션과 서버 환경을 만들어 동작 시키는 기능을 제공하는 소프트웨어 프레임워크
- 웹 어플리케이션을 실행시켜 필요한 기능을 수행하고 그 결과를 웹 서버에 전달
- Tomcat , Jeus , IBM WebSphere

![KakaoTalk_20211013_041308218](C:\Users\ayeong\Desktop\KakaoTalk_20211013_041308218.png)

1. Client가 WebServer에  HttpRequest를 보냄
2. 이것을 Web Server가 WebContainer에 위임함(웹서버와 소켓으로 통신)
3. WebContainer는 Servlet의 생명주기를 담당한다.
4. **멀티스레드**
   * Tomcat 서버가 다중 쓰레드를 생성,운영등 관리해주어 안정성에 대해 걱정하지 않아도 됨.
5. Servlet 인스턴스는 항상 1개만 존재->**Singleton Pattern**



**init() -> service()_doGet(),doPost() -> destory()**

* init() 메소드
  * 한번만 수행
  * servlet 객체 초기화 역할을 수행한다.
* service(request,response)메소드
  * request타입에 따라 doGet,doPost()가 대표적으로 실행됨
  * 메소드가 return되면 해당 thread는 제거됨
* destroy()메소드
  * 한번만 수행됨
  * WAS가 갱신되거나 종료될 때 호출된다.
  * Servlet객체를 메모리에서 제거하는 역할을 수행함.

<br />