<div align="center">
  <br />
  <h1>HTTP Header의 종류와 예시</h1>
  <br />
</div>

## 목차

1. [**HTTP Message**](#1)
2. [**General Header**](#2)
3. [**Request Header**](#3)
4. [**Response Header**](#4)
5. [**Entity Header (Representation)**](#5)
6. [**Cookie**](#6)

<br />

<div id="1"></div>

## HTTP Message

> HTTP에서 교환하는 정보

- **[HTTP Header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)**: HTTP 전송시 서버와 클라이언트에게 필요한 모든 부가 정보
  - `헤더 필드 명 : 필드 값` 구조. 여러 개의 필드 값이 존재 가능하다.
  - 과거 RFC2616 분류: `General Header`, `Request Header`, `Response Header`, `Entity Header`
- **Empty Line(CR+LF)**: 헤더와 메시지 바디 구분
- **HTTP Body**: 전송되어야 하는 데이터 자체. 항상 존재하는 건 아니다.

<img src="../images/http_msg_structure.PNG" alt="http_msg_structure" />


<br />

<div id="2"></div>

## General Header

> 리퀘스트 메시지와 리스폰스 메시지에 적용되는 기본적인 정보

- **Date**: 메시지가 생성된 날짜
  - `Date: Tue, 10 Aug 2021 15:40:02 GMT`
- **Transfer-Encoding**: 분할 전송. 메시지 바디의 전송 코딩 형식을 지정한다.
  - `Transfer-Encoding: chunked`

<br />

<div id="3"></div>

## Request Header

> 요청 정보. 리퀘스트 메시지에 사용되는 헤더로 Request Line, Request Header, General Header, Entity Header로 이루어져 있다.

- `협상` `(콘텐츠 네고시에이션 Content Negotiation)`: 클라이언트가 선호하는 표현을 요청함으로써 클라이언트에게 더 적합한 리소스를 제공한다.
- **Accept**: 콘텐츠가 선호하는 미디어 타입
  - `Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8`
- **Accept-Charset**: 클라이언트가 선호하는 문자 인코딩
- **Accept-Encoding**: 클라이언트가 선호하는 압축 인코딩 방식
  - `Accept-Encoding: gzip, deflate, br` 
- **Accept-Language**: 자연 언어 우선 순위
  - `Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7`
- `Quality Values(q)`: q값이 클수록 또는 구체적일수록 높은 우선 순위를 가지며, q=1은 생략 가능하다.

<br />

- **Host**: 요청한 호스트 정보(도메인). 하나의 IP 주소에 여러 도메인이 적용되어 있는 경우를 구분하며 필수 헤더다.
  - `Host: edu.ssafy.com`
- **User-Agent**: 클라이언트 애플리케이션의 명칭 및 버전 정보. 어떤 종류의 브라우저에서 장애가 발생하는지 파악이 가능하며 통계에 많이 사용된다.
  - `User-Agent: Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.131 Mobile Safari/537.36`
- **Referer**: 직전 웹페이지 주소. 유입 경로 분석이 가능하며 referrer의 오타다.
  - `Referer: https://edu.ssafy.com/`

<br />

<div id="4"></div>

## Response Header

> 응답 정보. 특정 유형의 리스폰스 메시지에 사용되는 헤더로 Status-Line, Response Header, General Header, Entity Header로 이루어져 있다.

- **Server**: 요청을 처리하는 origin 서버의 소프트웨어 정보
- **Location**: 페이지 리다이렉션. 3xx 응답의 결과에 Location 헤더가 있다면 Location 위치로 리다이렉트한다.
- **Retry-After**: 유저 에어전트가 다음 요청을 하기까지 기다려야 하는 시간(날짜 또는 초단위)

<br />

<div id="5"></div>

## Entity Header (Representation)

> 표현. 리퀘스트 메시지와 리스폰스 메시지에 사용되는 표현 데이터를 해석하는데 사용한다. RFC723X부터 표현으로 용어가 변경되었다.

- **Content-Type**: 표현 데이터의 미디어 타입 형식 (`text/html;charset=utf-8`, `application/json`, `image/png`)
  - `Content-Type: text/html;charset=utf-8`
- **Content-Encoding**: 표현 데이터의 압축 방식. 데이터 보낼 때 메시지 바디를 압축 후 인코딩 헤더를 추가하고, 읽는 쪽에서 해당 정보로 압축을 해제한다. (`gzip`, `deflate`, `identity`)
  - `content-encoding: br`
- **Content-Language**: 표현 데이터의 자연 언어 (`ko`, `en`, `en-US`)
  - `Content-Language: ko-KR`
- **Content-Length**: 표현 데이터의 길이. 한번에 요청하고 한번에 받는다. Transfer-Encoding 때는 사용하지 못한다.

<br />

<div id="6"></div>

## Cookie

> 사이트에 방문할 때 해당 사이트가 사용하는 서버가 인터넷 사용자의 컴퓨터에 설치되는 작은 데이터 조각. 쿠키의 정보는 항상 서버에 전송되니 최소한의 정보만 전달한다.

- **Set-Cookie**: 서버에서 클라이언트로 쿠키 전달 (응답)
  - `set-cookie: 1P_JAR=2021-08-10-16; expires=Thu, 09-Sep-2021 16:21:40 GMT; path=/; domain=.google.com; Secure; SameSite=none`
- **Cookie**: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달
  - path: 이 경로를 포함한 하위 경로 페이지만 쿠키 접근 가능하다. 일반적으로 path=/ 루트로 지정한다.
- **Secure**: 쿠키는 http와 https 구분하지 않고 전송하지만 Secure 적용하면 https에만 전송

<br />
<br />

###### 출처: [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/), [그림으로 배우는 Http & Network Basic](https://book.naver.com/bookdb/book_detail.nhn?bid=8657832), [HTTP 헤더의 종류 및 항목](https://gmlwjd9405.github.io/2019/01/28/http-header-types.html)

<br />
<br /> 
