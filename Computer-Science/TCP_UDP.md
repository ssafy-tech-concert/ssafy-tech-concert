<div align="center">
  <br />
  <h1>TCP와 UDP</h1>
  <br />
</div>

## 목차

1. [**TCP**](#1)
2. [**TCP의 특징**](#2)
3. [**UDP**](#3)
4. [**UDP의 특징**](#4)
5. [**TCP vs UDP**](#5)
6. [**HTTP3와 UDP**](#6)

<br />

<img src="https://user-images.githubusercontent.com/56222478/146769576-440a35a4-c30b-4c93-84b9-6111cf49b975.png" style="width:500px;height:250px" />

> TCP와 UDP는 TCP/IP의 전송계층에서 사용되는 프로토콜이다. 전송계층은 패킷의 오류를 검사하고 재전송 요구 등의 제어를 담당하는 계층이다.

++ [https://www.youtube.com/watch?v=1pfTxp25MA8](https://www.youtube.com/watch?v=1pfTxp25MA8)

---

<br />

<div id="1"></div>

## TCP (Transmission Control Protocol, 전송제어 프로토콜)

대부분의 인터넷 응용 분야들은 신뢰성과 순차적인 전달을 필요로 한다.

TCP는 신뢰성이 없는 인터넷을 통해 종단간에 신뢰성 있는 바이트 스트림을 전송 하도록 특별히 설계되었다.

TCP 서비스는 송신자와 수신자 모두가 소켓이라고 부르는 종단점을 생성함으로써 이루어진다.

모든 TCP 연결은 전이중, 점대점 방식이다.

전이중이란 전송이 양방향으로 동시에 일어날 수 있음을 의미하며 점대점이란 각 연결이 정확히 2 개의 종단점을 가지고 있음을 의미한다.

1:1 통신만 가능하다.

<br />

<div id="2"></div>

## TCP의 특징

- 신뢰성 있는 데이터 전송을 지원하는 연결 지향형 프로토콜이다.
- 사전에 3-way handshake라는 과정을 통해 연결을 설정하고 통신을 시작한다.
- 4-way handshake 과정을 통해 연결을 해제한다.
- 흐름 제어, 혼잡 제어, 오류 제어를 통해 신뢰성을 보장한다. 그러나 이 때문에 UDP보다 전송 속도가 느리다는 단점이 있다.
- 데이터의 경계를 구분하지 않는다. (바이트 스트림 서비스)
- 데이터의 전송 순서를 보장하며 수신 여부를 확인할 수 있다.
- TCP를 사용하는 예로는 대부분의 웹 HTTP 통신, 이메일, 파일 전송에 사용된다.

- 흐름제어, 혼잡제어, 오류제어
    
    **흐름 제어**
    
    - 송신측과 수신측의 데이터 처리 속도 차이를 해결하기 위한 기법
    - receiver가 packet을 지나치게 많이 받지 않도록 조절하는 것
    - receiver가 sender에게 현재 자신의 상태를 feedback 한다
    
    **혼잡 제어**
    
    - 송신측의 데이터 전달과 네트워크의 데이터 처리 속도 차이를 해결하기 위한 기법
    - 흐름제어가 송신측과 수신측 사이의 전송속도를 다루는데 반해, 혼잡제어는 호스트와 라우터를 포함한 보다 넓은 관점에서 전송 문제를 다루게 된다.
    
    **오류 제어**
    
    - 훼손된 패킷을 감지 하고 중복 수신 된 패킷을 확인 후 폐기하며, 손실된 패킷은 재전송하고 순서에 맞지 않는 세그먼트를 버퍼에 저장하는 일을 한다.
    
    [https://rok93.tistory.com/entry/네트워크-TCP-흐름제어혼잡제어](https://rok93.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCP-%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4)
    

---

<br />

<div id="3"></div>

## UDP (User Datagram Protocol, 사용자 데이터그램 프로토콜)

UDP는 비연결형 프로토콜 이다.

IP 데이터그램을 캡슐화하여 보내는 방법과 연결 설정을 하지 않고 보내는 방법을 제공한다.

데이터 그램 : 독립적인 관계를 지니는 패킷

UDP는 흐름제어, 오류제어 또는 손상된 세그먼트의 수신에 대한 재전송을 하지 않는다.

이 모두가 사용자 프로세스의 몫이다.

종종 클라이언트는 서버로 짧은 요청을 보내고, 짧은 응답을 기대한다.

만약 요청 또는 응답이 손실된다면, 클라이언트는 time out 되고 다시 시도할 수 있으면 된다.

코드가 간단할 뿐만 아니라 TCP의 초기설정에서 요구되는 프로토콜보다 적은 메시지가 요구된다.

<br />

<div id="4"></div>

## UDP의 특징

- 데이터를 데이터 그램 단위로 처리하는 프로토콜.
- 비연결형 프로토콜로 사전에 연결 설정 없이 데이터를 전달한다.
- 사전에 연결 설정을 하지 않은 데이터 그램 방식을 통해 데이터를 전달하기 때문에 하나의 메시지에서 분할된 각각의 패킷은 서로 다른 경로로 전송될 수 있다.
- 송신측에서 전송한 패킷의 순서와 수신측에 도착한 패킷의 순서가 다를 수 있다. 그러나 서로 다른 경로로 패킷을 처리함에도 불구하고 순서를 부여하거나 재조립하지 않는다.
- 흐름 제어, 혼잡 제어, 오류 제어를 하지 않으므로 손상된 세그먼트에 대한 재전송을 하지 않는다.
- 이로 인해 속도가 빠르며 네트워크 부하가 적다는 장점이 있지만, 신뢰성 있는 데이터 전송을 보장하지 못한다.
- UDP는 DNS(누군가 DNS 서비스를 요청할 때마다 TCP처럼 Session을 맺고 통신한다면 속도도 느리고, 서버 리소스도 엄청나게 소모될 것이다.) 등에서 사용된다

<br />

<div id="5"></div>

## TCP vs UDP

먼저, TCP의 데이터 송신 과정을 살펴보자.

<img src="https://madplay.github.io/img/post/2018-02-04-network-tcp-udp-tcpip-2.png" style="width:400px;height:400px" />

반면, UDP는 일방적이다.

<img src="https://madplay.github.io/img/post/2018-02-04-network-tcp-udp-tcpip-3.png" style="width:400px;height:400px" />

즉, **신뢰성이 요구되는 애플리케이션에서는 TCP를 사용**하고 **간단한 데이터를 빠른 속도로 전송하고자 하는 애플리케이션에서는 UDP를 사용**한다.

<!-- ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dc2a516c-d25c-4d43-86db-af9653d527e0/Untitled.png) -->
<img src="https://user-images.githubusercontent.com/56222478/146770426-a7ae7b3c-9396-4144-9524-4f6988321e5c.png" style="width:550px;height:300px" />

<br />

<div id="6"></div>

## HTTP3 와 UDP

<img src="https://user-images.githubusercontent.com/56222478/146770632-af4c8938-2238-404b-a648-f9e6dabe8590.png" style="width:550px;height:350px" />

[https://evan-moon.github.io/2019/10/08/what-is-http3/](https://evan-moon.github.io/2019/10/08/what-is-http3/)
