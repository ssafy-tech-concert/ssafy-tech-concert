<div align="center">
  <br />
  <h1>SOLID</h1>
  <br />
</div>

## 목차

1. [**SOLID 원칙**](#1)
2. [**SRP: 단일 책임 원칙(Single Responsibility Principle)**](#2)
3. [**OCP: 개방-폐쇄 원칙(Open-Closed Principle)**](#3)
4. [**LSP: 리스코프 치환 원칙(Liskov Subsitution Principle)**](#4)
5. [**ISP: 인터페이스 분리(Interface Segregation Principle)**](#5)
6. [**DIP: 의존성 역전 원칙(Dependency Inversion Principle)**](#6)

<br />

<div id="1"></div>

## SOLID 원칙

- SOLID 원칙의 등장 : 로버트 C. 마틴은 1980년대 후반부터 소프트웨어 설계 원칙에 대해 이야기를 나누었고, 2000년대 초반에 안정화된 버전을 내놓았다. 그리고 2004년 마이클 페더스가 원칙들을 재배열하여 SOLID라는 단어를 만들면서 탄생했다.
- SOLID 원칙
  - SRP: 단일 책임 원칙(Single Responsibility Principle
  - OCP: 개방-폐쇄 원칙(Open-Closed Principle)
  - LSP: 리스코프 치환 원칙(Liskov Subsitution Principle)
  - ISP: 인터페이스 분리(Interface Segregation Principle)
  - DIP: 의존성 역전 원칙(Dependency Inversion Principle)
- SOLID 원칙의 목적 : 모듈 수준의 소프트웨어 구조가 다음과 같도록 한다
  - 변경에 유연하다
  - 이해하기 쉽다 
  - 많은 소프트웨어 시스템에 사용될 컴포넌트의 기반이 된다

<br />

<div id="2"></div>

## SRP: 단일 책임 원칙(Single Responsibility Principle)

> 소프트웨어 모듈의 변경의 이유는 하나여야 한다
- 클래스를 변경하기 위한 이유가 두 가지 이상이라면 이 원칙을 위배하는 것
- 하나의 모듈은 하나의, 오직 하나의 액터에 대해서만 책임져야 한다
  - 액터 : 시스템이 동일한 방식으로 변경되기를 원하는 사용자들이나 이해관계자들
  - 모듈 : 소스 파일 또는 단순히 함수와 데이터 구조로 구성된 응집된 집합
- 데이터와 메서드 분리 & 중요한 업무 규칙은 데이터와 가깝게 배치
- 메서드와 클래스 수준의 원칙

<br />

<div id="3"></div>

## OCP: 개방-폐쇄 원칙(Open-Closed Principle)

> 소프트웨어 개체는 확장에는 열려 있고, 변경에는 닫혀 있어야 한다     
> 기존 코드를 수정하기보다는 새로운 코드를 추가하는 방식으로 설계해야 소프트웨어 시스템을 쉽게 변경할 수 있다
- 처리 과정을 클래스 단위로 분할 및 컴포넌트 단위로 구분
- 컴포넌트 관계는 단방향으로 구성
- 시스템 확장은 쉽게 하면서 변경으로 인한 영향은 최소화하는 것이 목적
- 시스템을 컴포넌트 단위로 적절히 분리하고, 저수준 컴포넌트의 변경으로부터 고수준 컴포넌트를 보호할 수 있는 형태로 의존성 계층구조가 만들어지도록 한다

<br />

<div id="4"></div>

## LSP: 리스코프 치환 원칙(Liskov Subsitution Principle)

> 상호 대체 가능한 구성요소로 소프트웨어를 만들기 위해서는 반드시 서로 치환 가능해야 한다
- 정사각형/직사각형 문제
  - `Rectangle`은 `setHeight`, `setWidth` 2개의 메서드가 있지만, `Sqaure`은 `setSide`로 1개의 메서드만 있는 경우다. 이때 `Square`은 `Rectangle`의 하위 타입으로 적합하지 않다. `Sqaure`일 때를 대비해 `if문`을 넣는다면 `Rectangle`과 소통하는 `User`의 행위는 사용하는 타입에 의존하게 된다
  - 사각형 객체를 만들어서 각각 상속받는 것으로 해결할 수 있다
- 부모 객체를 상속한 자식 객체는 부모 객체를 대신할 수 있다

<br />

<div id="5"></div>

## ISP: 인터페이스 분리(Interface Segregation Principle)

> 소프트웨어 설계자는 사용하지 않는 것에 의존하지 않는다
- 불필요한 내용을 많이 포함한 모듈에 의존하는 것은 좋지 않다 → 해당 모듈 때문에 불필요하게 재컴파일/재배포가 일어날 수 있기 때문
- 기본 이어폰에 노이즈캔슬 기능까지 넣는다면 노이즈캔슬 기능이 없는 이어폰은 해당 기능을 무효로 하도록 해야한다. 이를 해결하려면 기본 이어폰은 듣기 기능만 넣고, 노이즈캔슬 기능은 필요한 이어폰만 상속받으면 된다.
- 소스 코드 의존성이 적어야 상대적으로 유연하고 결합도가 낮은 시스템을 만들 수 있다
- 객체는 반드시 필요한 기능만 가져야 하며, 필요에 따라 인터페이스를 분리해야 한다

<br />

<div id="6"></div>

## DIP: 의존성 역전 원칙(Dependency Inversion Principle)

> 고수준 정책을 구현하는 코드는 저수준에 의존해서는 안되고, 세부사항이 정책에 의존해야 한다
- 변동성이 큰 구현체에 덜 의존하고 안정된 추상 인터페이스를 선호하는 안정된 소프트웨어 아키텍처를 만들자
  - 변동성이 큰 구체 클래스를 참조하는 것을 최소화하고 추상 인터페이스를 참조한다
  - 변동성이 큰 구체 클래스로부터 파생하지 않는다
  - 구체 함수를 오버라이드를 하지 않는다. 오버라이드 때문에 의존성이 발생할 수 있다
- DIP 위배를 모두 없앨 수는 없지만, DIP를 위배하는 클래스들을 일부 구체 컴포넌트 내부로 모아서 시스템의 나머지와 분리할 수는 있다
- 구체적이고 변동성이 크다면 절대 그 이름을 언급하지 말자

<br />
<br />

###### 출처: [클린 아키텍처(로버트 C. 마틴 지음, 송준이 옮김, 인사이트, 2021)](http://www.yes24.com/Product/Goods/77283734), [SOLID 원칙](https://johngrib.github.io/wiki/jargon/solid/)

###### 함께 보면 좋은 자료: [객체지향 5원칙 : SOLID](https://jaeyeong951.medium.com/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5-5%EC%9B%90%EC%B9%99-solid-ac7d4d660f4d), [[OOP] 객체지향 5원칙(SOLID) - 인터페이스 분리 원칙 (Interface Segregation Principle)](https://blog.itcode.dev/posts/2021/08/16/interface-segregation-principle), [[OOP] 객체지향 5원칙(SOLID) - 리스코프 치환 원칙 (Liskov Subsitution Principle)](https://blog.itcode.dev/posts/2021/08/15/liskov-subsitution-principle)

<br />
<br />
