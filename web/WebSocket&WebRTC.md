### 1. 기존 HTTP 의 동작 개념
![](https://images.velog.io/images/alstjdwo1601/post/6ab32629-e0d6-4d53-80a7-65f94f8d164f/image.png)

기존의 HTTP 통신은 클라이언트의 HTTP Request 를 받은 웹 서버가 Response를 보내주는 방식입니다. 클라이언트가 브라우저를 통해 특정 페이지를 요청하면(Request) 페이지를 구성하는 모든 자료를 서버가 보내줍니다.(Response)

이때 서버는 클라이언트의 Request가 없다면 직접적으로 클라이언트에게 정보를 보낼 수 없습니다.
또한, 한번 Request - Response 의 사이클이 지나면 브라우저 - 서버의 통신은 끝납니다.

만약 이러한 HTTP 통신을 이용하여 채팅앱을 만든다면 상대방의 메시지를 읽기 위해 매번 새로고침을 해서 서버에 Request 를 날리고 Response를 받아야 할겁니다. 

**즉, 실시간 통신을 필요로하는 프로그램에서 HTTP는 한계를 보입니다.**

HTTP 는 실시간 서비스를 위해 Polling 이라는 기술을 썼습니다. 일정 주기로 서버에 Request를 보내는 형식인데, 이로 인해 불필요한 Request와 커넥션이 생길 수 있습니다.

이를 개선한 Long Polling 이라는 기술은 이벤트가 발생하는 경우에만 서버에서 Response를 하는 방식이지만 이 역시 많은 커넥션이 생기면 Polling 과 동일한 문제점을 가진다.

-----------------------


### 2. Web Socket 의 등장
![](https://images.velog.io/images/alstjdwo1601/post/a0bf8186-e626-48c0-97eb-555892b76de6/image.png)

웹 소켓은 이러한 HTTP 의 한계를 개선하기 위해 등장했습니다. 기존의 Request - Response 구조를 대신하여 커넥션이 Open 되어있는지 Close 되어있는지를 체크합니다.
즉 브라우저가 서버와의 통신을 Open 하면 **양방향 통신**이 자유롭게 일어나며 원할 때까지 통신이 유지됩니다.

 
![](https://images.velog.io/images/alstjdwo1601/post/aa2ad8a7-94d4-4dac-bd91-7413500dcae0/image.png)
다만 웹 소켓도 최초 접속시에는 HTTP 프로토콜 위에서 핸드쉐이킹을 합니다.
특이점은 반드시 GET 메서드를 이용하며
Upgrade : websocket 이라는 헤더를 통해 앞으로 웹소켓 통신을 할 것이라고 명시하며
Connection : Upgrade 라는 헤더는 위의 Upgrade가 명시된 경우 필수적으로 포함해야합니다.

**웹 소켓에서는 브라우저 서버 둘다 메시지를 보내고 받을 수 있습니다. 따라서 서버는 브라우저의 리퀘스트를 더이상 기다리지 않고 업데이트된 정보가 있다면 바로바로 브라우저에 전달합니다.**
또한 HTTP 헤더는 800바이트 ~ 수 KB 정도의 헤더 크기를 가지지만 Web Socket 은 몇 바이트 정도로 압축이 가능합니다.

이러한 실시간 통신의 장점을 활용하여 채팅앱, 주식&코인 거래앱, 게임에서 많이 쓰이고 있습니다.

또한 기존의 XMLHttpRequest + Server-Sent Event 를 조합하여 양방향 통신을 구현하던 AJAX 에 비해 설계과 구현이 간단하다는 장점이 있습니다.

 
 ---------------------------

### 3. Web Socket 서버

![](https://images.velog.io/images/alstjdwo1601/post/ae5ff333-b757-48f8-9a4c-33147cfda3e7/image.png)

우리가 단톡방에 들어간다면 실제로 단톡방에 있는 사람들과 직접적으로 통신이 연결되는게 아닙니다.

위의 그림과 같이 공통의 웹 소켓 서버에 입장하게 되는 구조입니다. 따라서 메시지를 웹 소켓 서버에 먼저 보낸 후, 서버는 그 메시지를 다른 사람들에게 전달해줍니다.

이 경우 웹 소켓 서버의 성능이 매우 중요합니다. 거의 실시간에 가깝게 데이터를 커넥션에 연결된 사람들에게 포워딩해야 하기 때문에 서버에 들어가는 비용이 증가합니다. 또한 서버에 실시간으로 사람이 많이 입장하게 된다면 딜레이가 생길 수 밖에 없고 서버가 내려간다면 모든 통신이 불가능해지는 단점을 가집니다.

그리고 항상 연결상태를 유지하는 Stateful 한 기술이기에 부하가 생길 수 있습니다.

-----------------------------------------

### 4. WebRTC 란?
![](https://images.velog.io/images/alstjdwo1601/post/a171e99c-51d6-41ca-bd5b-40bd90d877bd/image.png)

WebRTC(Web Real Time Communication) 란 중간에 서버를 두지않고 클라이언트들의 브라우저가 직접 연결되는 기술입니다.

쉽게 말하면 추가적인 드라이버, 플러그인과 같은 소프트웨어 설치없이 p2p 연결로 데이터 교환을 가능하게 합니다.

이를 이용해 화상 회의 프로그램 , 실시간 스트리밍, 스크린 공유 등의 서비스가 탄생하게 되었습니다.

WebRTC는 서버를 통하지 않기 때문에 속도가 더 빠르고 Web Socket 이 가지는 단점을 개선했습니다. 

(중개 서버는 아니지만 각 개인 컴퓨터는 ip가 존재하고 상대의 ip주소를 알아야 데이터 교환이 가능하다. 그러나 개인 컴퓨터는 방화벽 등의 보호장치가 있어서 Stun/Turn 서버를 이용한다.
https://alnova2.tistory.com/1110 에 더 자세한 내용이 담겨있다. )

다만, 이 또한 단점을 가지는데 예를 들어 웹엑스와 같은 화상 채팅방에 사람이 많이 입장한다면 그 모든 영상을 다운받아야 하며 나의 영상을 전부에게 업로드 해주어야 한다.

즉, WebRTC 기술은 수 많은 사람들이 쓰기에는 제약이 있기에 확장성이 낮습니다.

다만 이 두 가지 기술은 리얼타임 서비스를 구현할 수 있게 해주며 전부 Javascript 를 통해 배울 수 있다고 합니다.


--------------------------------------------------------
<참고>
https://velog.io/@wldus9503/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-Network3.-WebSocket-%EC%9B%B9-%EC%86%8C%EC%BC%93%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C

https://www.youtube.com/watch?v=5EhsjtBE7I4&t=333s

https://wormwlrm.github.io/2021/01/24/Introducing-WebRTC.html

https://www.youtube.com/watch?v=MPQHvwPxDUw

https://ohgyun.com/436
