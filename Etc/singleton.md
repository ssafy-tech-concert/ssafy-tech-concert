<div align="center">
  <br />
  <h1>싱글톤 패턴</h1>
  <br />
</div>

## 목차

1. [**싱글톤(Singleton) 패턴?**](#1)
2. [**싱글톤 패턴 사용 이유**](#2)
3. [**싱글톤 패턴 문제점**](#3)

<br />

[**백기선님의 유튜브 채널을 참고하여 글을 작성하였습니다.**](https://www.youtube.com/watch?v=OwOEGhAo3pI%20)

<br>
<div id="1"></div>

**싱글톤(Singleton) 패턴?**

-   객체의 인스턴스가 오직 한 개만 생성되는 패턴
-   **GOF 디자인 패턴**의 일종으로 생성, 구조, 행위 중 **생성 패턴에** 해당

**👉 관련 용어 정리**

**Thread** : 프로세스가 할당받은 자원을 이용하는 실행의 단위

**Multi-Thread** : 하나의 프로세스 내에서 둘 이상의 스레드가 동시에 작업을 수행하는 것

**Thread-Safe** : 멀티 스레드 프로그래밍에서 함수, 변수, 객체가 여러 스레드로부터 동시에 접근되어도 프로그램 실행에 문제가 없음을 의미  
**Side-Effect** : 원래의 목적과 다른 효과 또는 부작용 = 버그

**Synchronized** : 여러개의 스레드가 한개의 자원을 사용하고자 할 때, **현재** **데이터를** **사용하고** **있는** **해당** **스레드를** **제외하고** **나머지** **스레드들은** **데이터에** **접근** **할** **수** **없도록** **막는** **개념**

**Lazy Loading** : 당장 필요하지 않은 리소스들을 추후에 로딩하게 하는 기술

****싱글톤 적용 안 한 코드****

```
NotSingleton n1 = new NotSingleton();
NotSingleton n2 = new NotSingleton();
System.out.println(n1==n2);
```

결과 : false

-   new 연산자를 사용하면 새로운 인스턴스를 만들기 때문에 다르다고 나온다

**싱글톤 적용 코드 첫 번째 : 가장 일반적인 방법**

```
public class Singleton {

    private static Singleton instance;

    private Singleton(){}

    public static Singleton getInstance(){
        if (instance==null){//null이면 만들고
            instance = new Singleton();
        }
        return instance; // 아니면 만들지 않는다.
    }
}
```

```
Singleton s1 = Singleton.getInstance();
Singleton s2= Singleton.getInstance();
System.out.println(s1==s2);
```

결과 : true

-   new를 사용하지 않고 객체를 생성하려면 클래스 안에 Private로 설정
-   싱글톤 객체를 글로벌하게 사용하려면 Static 한 메서드를 사용

이 코드의 문제점

-   우리는 웹 애플리케이션을 만든다면 멀티스레드 환경에서 작동한다.
-   이 코드는 멀티쓰레드 환경에서 안전하지 않는다. == Tread-Safe 하지 않다.
-   두 개가 있다고 가정했을 때 동시에 getInstance()를 호출한다면 값이 달라진다.

**싱글톤 적용 두 번째 : Thread-Safe 하게 구현하기**

**Thread-Safe - 1**

```
public class Singleton {

    private static Singleton instance;

    private Singleton(){}

    public static synchronized Singleton getInstance(){
        if (instance==null){
            instance = new Singleton();
        }
        return instance;
    }
}
```

-   Synchronized(동기화 처리) 키워드 쓰기
-   메서드의 한 번에 딱 하나의 스레드만 들어오도록 해주는 것 
-   멀티 스레드 환경에서도 하나의 인스턴스만 보장.
-   getInstance() 메서드 호출 시 동기화를 처리하는 작업 때문에 성능에 불이득이 있을 수 있다.

**Thread-Safe - 2**

```
public class Singleton {

    private static final Singleton INSTANCE = new Settings();

    private Singleton(){}
    
    public static synchronized Singleton getInstance(){
        return INSTANCE;
    }
}
```

-   이른 초기화
-   객체를 만드는 비용이 비싸지 않는다면 사용해 볼만하다. 
-   미리 만든다는 의미 애플리케이션 로딩 시 많은 리소스가 필요할 수 있다는 단점이 있음.

**Thread-Safe-3**

```
public class Singleton {

    private static volatile Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

-   Double checked locking //효율적인 동기화 블록 만들기
-   Static 변수에 volatile(볼랫틀)을 만들어 주어야 함//java 1.5 이상에서만 동작한다. 
-   인스턴스가 있을 경우 sycronized를 안 쓴다.
-   성능에 유리하다.
-   인스턴스를 필요로 하는 시점에만 만들 수 있다.
-   단점은 기법이 복잡하다. 볼랫틀을 이해하고 싶다면 자바 메모리 기법 공부를 좀 해야 한다. 

**Thread-Safe-4**

```
public class Singleton {

    private Singleton() {}

    private static class SingletonHolder{ // static inner class 선언
        private static final Singleton INSTANCE = new Singleton();
    }
    public static Singleton getInstance(){
        return SingletonHolder.INSTANCE;
    }
}
```

-   진짜 권장하는 방법
-   Static inner 클래스 사용하기
-   이렇게 하면 멀티 스레드 환경에서도 안전하고 Lazy Loading 도 가능하다. 코드가 많아 지지도 않는다.
<br>
<div id="2"></div>

****싱글톤 패턴 사용 이유****

-   최초 한 번의 new 연산자를 통해서 고정된 메모리 영역을 사용하기 때문에 추후 해당 객체에 접근할 때 메모리 낭비 방지
-   전역으로 사용되는 인스턴스이기 때문에 데이터 공유가 쉬움
-   이미 생성된 인스턴스를 활용하기 때문에 속도에서 이점이 있다.
<br>
<div id="3"></div>

****싱글톤 패턴 문제점****

-   동시성 문제
    -   멀티스레딩 환경에서 싱글톤 인스턴스에 동시에 접근하게 되면 동시성 문제가 발생
    -   Syncronized로 해결
-   자식 클래스 못 만듦
-   내부 상태 변경이 어려움
-   **다른 객체 간의 결함도**가 높아져서 객체 지향 설계 원칙에 어긋나게 된다.
    -   객체지향 설계 원칙 SOLID 중 DIP, OCP 위반  
    -  의존 관계 역전 원칙 **DIP** : 저수준 모듈이 고수준 모듈에 의존하게 되는 것
    -   개방 폐쇄 원칙 **OCP :** 소프트웨어는 확장에 열려야 하고 수정에는 닫혀 있어야 한다.

**정리**

싱글톤 패턴은 멀티 스레딩 환경에서도 동작이 가능해야 하기 때문에 Thread-Safe가 보장되어야 한다.

우리가 사용하는 Spring 컨테이너는 싱글톤 컨테이너이다 즉 싱글톤 패턴을 적용하지 않아도 빈을 싱글톤으로 관리한다.