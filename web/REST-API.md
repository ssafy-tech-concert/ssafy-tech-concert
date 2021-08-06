

REST

Representational State Transfer

표현 상태 전달

일종의 HTTP에 디자인패턴

HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP

Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을

적용하는 것을 의미한다.

• URI : **인터넷에 있는 자원을 나타내는 유일한 주소** \*

• **HTTP(HyperText Transfer Protocol) : W3 상에서 정보를 주고받을 수 있는 프로토콜이다.**

**주로 HTML 문서를 주고받는 데에 쓰인다.**





REST 구성 요소

자원(Resource): URI모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에

존재한다.자원을 구별하는 ID는 ‘/products/:product\_id’와 같은 HTTP URI

다.Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한

조작을 Server에 요청한다.

행위(Verb): HTTP Method HTTP 프로토콜의 Method를 사용한다.HTTP 프로토콜은

GET, POST, PUT, DELETE 와 같은 메서드를 제공한다.

표현(Representation of Resource): Client가 자원의 상태(정보)에 대한 조작을

요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.REST에서 하나의

자원은 JSON, XML, TEXT 등 여러 형태의 Representation으로 나타내어 질 수

있다.JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.





Request

Response





REST 왜 사용할까?

어플리케이션 분리 및 통합 , 모든 디바이스 통신 가능





REST 제약 조건

클라이언트- 서버 (Client-Server)

\- 클라이트와 서버의 기능은 완벽히 분리되어야 한다.

무상태 (Stateless)

\- REST는 HTTP의 특성을 이용하기 때문에 무상태성을 갖는다. 즉 서버에서 어떤 작업을 하기

위해 상태정보를 기억할 필요가 없고 들어온 요청에 대해 처리만 해주면 되기 때문에 구현이

쉽고 단순해진다.

캐시 처리 가능

\- 클라이언트는 응답을 캐싱할 수 있어야 한다. —> 클라이언트가 같은 자료를 중복 요청하는

것을 막아 서버의 부담을 줄여줄 수 있다.





REST 제약 조건

계층화

\- 서버와 클라이언트 사이에 캐시 서버나 로드 밸런서 등의 중간 서버를 둘 수 있다.

\- 클라이언트는 대상 서버에 직접 연결되었는지, 혹은 중간 서버에 연결되었는지 알수 없다.

Code-On-Demand

\- 클라이언트는 서버에서 자바 애플릿 혹은 자바스크립트 실행 코드를 받아 기능을 일시적으로

확장할 수 있습니다.

인터페이스 일관성 (Uniform Interface)

\- 자원 식별 (ex http://localhost/api/read/books)

\- 메시지를 통한 리소스 조작 : HTTP메소드 를 통하여 서버측에 데이터를 컨트롤한다.

\- 자기 서술적 메시지 : REST API에서는 데이터에 대한 내용을 유추하는 것이 아닌 이 데이터를

설 명하는 명세서가 존재





로드밸런싱: 서버의 부하를 분산하기 위해 N개의 서버에 트래픽을 분배하는

것이다.









REST API

REST 기반으로 서비스 API를 구현한 것





REST API 특징

-사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과

재사용성을 높여 유지 보수 및 운용을 편리하게 할 수 있다.

-REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램

언어로 클라이언트, 서버를 구현할 수 있다.





REST API 설계 예시

HTTP Status Code(응답 코드, 상태 코드)

\- 클라이언트의 요청에 대해서 서버는 요청에 대한 처리 상태를 숫자 코드로 반환

•1 xx : (정보) 요청을 받았으며 프로세스를 계속한다

•2 xx : (성공) 요청을 성공적으로 받았으며 인식해서 처리했다

•3 xx : (리다이렉션) 요청 완료를 위해 추가 작업 조치가 필요하다.

•4 xx : (클라이언트 에러)요청의 문법이 잘못되었거나 요청을 처리할 수 없다.

•5 xx : (서버 에러) 서버가 명백히 요요한 요청에 대해 충족을 실패했다.

HTTP 메소드

\- 클라이언트가 요청을 보낼 때 해당 요청의 목적이 뭔지 HTTP 메소드를 통해 명시

•GET : 서버의 리소스를 조회하고자 할 때

•POST : 서버의 리소스를 생성하고자 할 때

•DELETE : 서버의 리소스를 삭제할 때

•PUT : 서버의 리소스를 수정하고자 할 때

•PATCH : 서버의 리소스의 부분만을 수정할 때





RESTful 이란?

RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해

사용되는 용어이다.

‘REST API’를 제공하는 웹 서비스를 ‘RESTful’하다고 할 수 있다.RESTful은

REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.

RESTful의 목적

이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것

RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니라 성능이

중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.

RESTful 하지 못한 경우

Ex1) CRUD 기능을 모두 POST로만 처리하는 API

Ex2) route에resource, id외의 정보가 들어가는 경우(/students/updateName)





