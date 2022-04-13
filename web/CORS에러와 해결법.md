![](https://images.velog.io/images/alstjdwo1601/post/5f559cd8-fcd3-4424-9c05-ff92d4c71cf0/image.png)

CORS (Cross-Origin Resource Sharing)는 **교차 출처 리소스 공유**로 인해 생기는 에러입니다. 조금 더 쉽게 말하면 한 출처에서 실행중인 웹 애플리케이션이 다른 출처의 자원에 접근할때 이러한 에러가 발생합니다.

이 에러를 이해하기 위해서는 **출처**와 **SOP(Same-Origin Policy)** , **Preflight Request**에 대해 알아야합니다.

> 1. **출처는** Origin을 의미하는데 프로토콜 + 호스트 + 포트를 포함하는 개념입니다.

예를들어, **https//www.naver.com** 이라는 주소가 있다면 
1) **프로토콜**은 https://
2) **호스트**는 www.naver.com
3) **포트**는 localhost:8080 같은 경우 8080을 의미합니다.

 <출처 비교 예시>
https://github.com/ssafy-tech-concert/ssafy-tech-concert/blob/master/web/CORS.md

------------

> 2. **SOP는 Same-Origin Policy** 즉, 동일 출처 정책입니다. 

위에서 언급한 주소의 프로토콜, 호스트, 포트가 모두 같다면 '**동일 출처**' 라고 부르며 동일 출처에서 가져온 리소스만을 허용함으로써 위험요소가 있는 다른 출처의 리소스를 제한하는 정책입니다. 

SOP에 의하면 API를 통해 리소스를 가져오는 웹 어플리케이션은 "**자신의 출처와 동일한 리소스**" 만 불러올 수 있습니다. 그래서 다른 출처의 리소스를 가져오려면 해당 출처에서 올바른 CORS 헤더를 포함한 응답을 반환해줘야 합니다.

SOP는 웹 애플리케이션이 가져온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 보안방식입니다. 이를 통해 잠재적으로 문제를 발생시키는 공격 경로를 줄여줍니다.


> 3. **Preflight Request** - 예비 요청

예비요청은 위의 SOP 즉, 동일 출처 정책을 위반하는 경우 예비요청을 통해 검증을 거치는 단계입니다.

이 단계는 대략 다음과 같다.
![](https://velog.velcdn.com/images/alstjdwo1601/post/f9797cbd-46ab-4d90-af95-0c6988a349f7/image.png)


다음의 사진은 fetch API를 사용해 브라우저에게 리소스를 받아오라는 명령을 내리면, 브라우저는 서버에게 Preflight Request를 먼저 보내봅니다. 서버가 이 요청에 대한 응답으로 어떤 것을 허용하고 금지하는지를 정보로 응답 헤더에 담아 브라우저에게 다시 보내줍니다.

이때 **Access-Control-Allow-Origin(HTTP의 응답 헤더)** 에 허용하는 url이 명시되어 있습니다.
Access-Control-Allow-Origin : * 이라면 모든 url을 허용한다는 의미입니다.

이후 브라우저는 서버가 보내준 응답에서 허용 정책을 비교한 후 요청이 가능하다면 진짜 요청을 보내서 리소스를 받아오는 것입니다.



![](https://images.velog.io/images/alstjdwo1601/post/ca5de7e5-afa9-4e6b-a822-5875acea285d/image.png)

> 그렇다면 CORS 에러는 왜 발생하는 것일까?
크게 두 가지 경우에 CORS 에러가 발생할 수 있습니다.

#### 1. 자바스크립트에서** ajax, fetch(), axios api**를 사용하여 데이터를 가져오는 경우


   https://velog.io/@kysung95/%EA%B0%9C%EB%B0%9C%EC%83%81%EC%8B%9D-Ajax%EC%99%80-Axios-%EA%B7%B8%EB%A6%AC%EA%B3%A0-fetch
    
  우선 Ajax는 Asynchronous JavaScript And XML의 약자입니다.
  서버와 클라이언트가 JS를 이용하여 비동기적으로 데이터를 주고 받는 기술입니다. 원하는 데이터만 매번 새로고침하지 않고도 받을 수 있다는 것이 장점.
  
  기존에 웹에서 리소스를 비동기로 요청할때 XHR(XML HTTP Request) 객체를 사용했었는데 이는 잘 디자인된 API가 아닙니다. 이를 보완하기 위해 HTTP 요청에 최적화되어있고 상태도 잘 추상화 된 API가 등장했는데 그것이 Axios와 fetch입니다.
  
  Axios는 Promise based HTTP client for the browser and node.js 즉, 노드와 브라우저를 위한 HTTP 통신 라이브러리이며 리액트에서 많이 선호됩니다.
  
  fetch는 자바스크립트 내장 라이브러리입니다. Axios와 달리 모듈설치가 필요 없지만 호환성이 떨어지고 Axios는 모듈설치를 해야하지만 호환성이 좋습니다.

#### 2. API로 다른 Origin 의 리소스를 가져오는 경우

![](https://images.velog.io/images/alstjdwo1601/post/cd1f8e5c-5799-49f2-894f-e78d10e5f091/image.png)

다음과 같은 에러 문구를 분석해보면, CORS 정책에 의해 요청이 실패했고 그 이유는 Preflight request의 응답으로 돌아온 응답 헤더에 **Access-Control-Allow-Origin(서버에서 허가하는 출처)와 현재 요청을 보내는 브라우저의 출처가 다르기 때문 **  이라고 합니다.

즉, 현재 요청받은 출처는 서버에서 허가하는 출처가 아니기에 CORS 정책에 의해 에러가 나게 됩니다.


> CORS 해결하기

그렇다면 다른 출처에서 리소스를 가져오고 싶다면 어떻게 해야할까.


## 1. 프록시 서버 이용하기


외부 API 를 사용하고 있다면 내가 서버를 제어할 수 없으므로 **HTTP의 응답 헤더인 Access-Control-Allow-Origin**을 설정 할 수 없습니다. 또한, 상황상 서버 구축하기에는 시간적이나 실력적으로 문제가 있을 수도 있습니다. 
따라서 CORS 를 해결하기 위해 이미 구축된 프록시 서버를 사용하면 중간에서 HTTP 응답헤더를 가로채고  Access-Control-Allow-Origin : '*' 를 설정해서 응답을 보내주면 됩니다.

![](https://velog.velcdn.com/images/alstjdwo1601/post/09f47742-36da-480a-896d-846e6665d402/image.png)

요청해야하는 URL 앞에 프록시 서버 URL을 붙여서 요청하면 간단하게 해결이 가능합니다.


## 2. 스프링에서 CORS 해결하기

위의 방식은 사실 궁여지책일뿐, 실제로 서버를 구축하고 있다면 프록시 서버로 우회할 필요는 없습니다.

스프링에서 예비요청(Preflight) 에서 검증이 실패하면 해결방법이 3가지 있습니다.
![](https://velog.velcdn.com/images/alstjdwo1601/post/44e5f0db-bde1-478f-9cae-2a2e12a74dd3/image.png)


---------------------------

![](https://velog.velcdn.com/images/alstjdwo1601/post/79383b51-ae04-4427-bc43-b0f6f960e33d/image.png)

javax.servlet 의 Filter를 하나 생성하고 response 헤더에 Access-Control를 작성해주면 됩니다.

![](https://velog.velcdn.com/images/alstjdwo1601/post/35740e86-5f0b-42e7-adcc-20b5f949ba5e/image.png)

@CrossOrigin를 컨트롤러에 설정해주면 되는 아주 간단한 방식입니다

![](https://velog.velcdn.com/images/alstjdwo1601/post/1397845e-7be2-4c77-aa38-1aca8790c900/image.png)


메인함수에 @Bean 으로 Configurer를 추가하고 registry에 url등을 입력해주면 됩니다.
