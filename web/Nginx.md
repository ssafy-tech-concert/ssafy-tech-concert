<div align="center">
  <br />
  <h1>Nginx</h1>
  <br />
</div>

##  목차

1. [**Nginx는 뭘까?**](#1)
2. [**Nginx 왜 사용 할까?**](#2)
3. [**Nginx 정리**](#3)


<br />

<br />

<div id="1"></div>

## **1\. Nginx는 뭘까?** 

엔진엑스 사용하는 곳

### **Naver, kakao, github, netflx 대형 급 아이티회사에서 씀**

#### **Web Server ❔** :  HTTP를 통해 웹 브라우저에서 요청하는 HTML 문서나 오브젝트(이미지 파일 등)을 전송해주는 서비스 프로그램을 말한다. (정적인 자원을 처리해주는 것!)

EX) Happy House Build 된 파일 , Vue.js index.html 이것이 정적 파일

#### **WAS ❔ :** 클라이언트 요청에 대해 동적인 처리가 이뤄진 후 응답.

EX) Happy House Backend Login-API

-   클라이언트에서 로그인 요청
-   웹 서버가 로그인 정보를 가지고 실제 로그인을 처리
-   WAS에서 로그인 처리 로직을 가지고 있음
-   이러한 과정을 진행해주는 것이 동적인 처리 즉 WAS의 역할!

**그렇다면 Nginx 는 Web Server 일까 WAS 일까?**

[##_Image|kage@cgfnqs/btrnB8bXUiW/ycsbbkeagUZ6w3WUP3qE31/img.png|CDM|1.3|{"originWidth":341,"originHeight":189,"style":"alignLeft","filename":"구조.PNG"}_##]

**Web Server 입니다.**

<div id="2"></div>

## **2\. Nginx 왜 사용 할까?**

-   **빠르다** 👍

[##_Image|kage@bhcf0I/btrnLIbf0tk/1Dcj3aUaCVGCSVUau5lVK0/img.png|CDM|1.3|{"originWidth":939,"originHeight":747,"style":"alignLeft","width":567,"height":451}_##]

X축 동시 요청 3천개의 동시 요청이 발생했을 때

Nginx 50개 요청일때랑 3000개 일때랑 메모리 사용량이 비슷함

아파치 요청이 많을때는 메모리수도 늘어난다

Nginx 는 메모리 사용량은 굉장이 효율적으로 사용한다.

[##_Image|kage@toZmp/btrnCByb6rw/ojm2934P5Kngt9xDLkJYN1/img.png|CDM|1.3|{"originWidth":936,"originHeight":703,"style":"alignLeft","width":587,"height":441}_##]

초당 요청 처리수

Nginx : 초당 처리를 12000개 할 수 있다.

동시 요청자가 많아 질수록 다른 것들에  비해서 초당 처리할 수 있는게 상당히 많다.

#### 👍 **점유율 : 이제는 Nginx**

[##_Image|kage@cYLvSx/btrnC3VywXH/U1czA0b5R7KxDzvVkejjpK/img.png|CDM|1.3|{"originWidth":880,"originHeight":430,"style":"alignLeft","width":645}_##]

-   **Reverse Froxy** ![](https://blog.kakaocdn.net/dn/bufZrE/btrnGjRlYTC/5lzRRa8aIk4jvBZyrHtq50/img.png)

✔ **Proxy :  대리 해주는거**

-   **forward Proxy** :
    -   Client와 Internet 사이 있음
-   **reverse Proxy** :  
    -   Internet과 appServer사이에 존재하는 서버
    -   요청에따른 처리를 어떤 서버로 할지 밸런싱있게 조율해주는 **로드밸런싱**이 가능하다 
        -    [##_Image|kage@p4BPC/btrnPDt2Paz/bu4gHEx9VfaaoEJWwxKDk0/img.jpg|CDM|1.3|{"originWidth":793,"originHeight":573,"style":"alignLeft","width":381,"height":275,"caption":"로드벨런싱","filename":"로드 밸런싱.jpg"}_##]
        -   캐시서버가 가능하다  👉 [캐시?](https://github.com/ssafy-tech-concert/ssafy-tech-concert/blob/master/web/Cache.md)
        -   자주 요청되는 클라이언트 요청을 저장(캐싱)해둘 수 있다.
        -   한번 더 요청있는 경우 백단까지 안가고 바로 응답 가능 
        -   보안 이점 : 외부에서 어디서 온 요청인지 알 수 없게끔 해준다. IP 숨기기 등과 같은거 

-   **SSL 지원**
    -   **웹사이트와 브라우저(혹은, 두 서버) 사이에 전송된 데이터를 암호화하여 인터넷 연결을 보안을 유지하는 표준 기술**

[##_Image|kage@ntQpo/btrnJBDYV4e/yCfejHOI9dmY6OCWIL7FF1/img.png|CDM|1.3|{"originWidth":940,"originHeight":340,"style":"alignLeft"}_##]

우리 사이트는 보안 처리가 잘 되어 있다 라는 것을 인증해주는 것 SSL이라는 **인증서**

**HTTPS도 Nginx를 쓰면 쉽게 설정 할 수 있다.**

-    비동기처리
    -   클라이언트의 요청을 비동기방식으로 처리 가능하도록해준다
    -   **이벤트루프** 사용
    -   👉 [비동기, 이벤트루프 참고자료](https://github.com/ssafy-tech-concert/ssafy-tech-concert/blob/master/Front-end/synchronous%26asynchronous.md)

<div id="3"></div>

정리

-   **Nginx는 적은 양의 자원으로 많은 양의 트래픽을 처리**할 수 있다. (👍 대량의 데이터를 처리할때 유리)
    -   **요청에 따라 추가적으로 자원을 사용하지 않기 때문에 많은 요청이 들어왔을 때 느려지지 않는다.**
    -   하지만 너무 많은 요청을 받으면 처리하지 못하는 것은 Apache와 마찬가지이다. 👎
        -   Nginx라도 당연히 무한대의 요청을 받을 수 있는 것은 아니다. 
    -   비동기로 **Context Switching이 적다.** 👍
        -   **Context Switching : 현재 진행하고 있는 Task(Process, Thread)의 상태를 저장하고 다음 진행할 Task의 상태 값을 읽어 적용하는 과정**
-   **우리 프로젝트에 Reverse Proxy (Nginx) 를 도입시 어떤 이점이 있을까?**  
    -   Reverse Proxy 위치에서 도입할 수 있는 기술들이 곧 이점
        -   캐싱, 로드 밸런싱, 보안 
    -   Client에게 실제 서버 ip를 숨길 수 있다.
        -   보안적으로 안전
        -   Client는 Reverse Proxy가 실제 Server라고 생각하고 접속하게 된다.
    -   우리 프로젝트에서 적용한 Reverse Proxy에서의 기능
        -   보안 (SSL, 실제 서버의 ip 숨기기 - redirect)
        -   캐싱 (to do)

참고자료

[비동기, 이벤트루프](https://github.com/ssafy-tech-concert/ssafy-tech-concert/blob/master/Front-end/synchronous%26asynchronous.md)

[캐시](https://github.com/ssafy-tech-concert/ssafy-tech-concert/blob/master/web/Cache.md)

[https://www.youtube.com/watch?v=ZJpT-Wa-pZ8](https://www.youtube.com/watch?v=ZJpT-Wa-pZ8)