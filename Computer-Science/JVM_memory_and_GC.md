<div align="center">
  <br />
  <h1>JVM메모리 구조와 가비지 컬렉터</h1>
  <br />
</div>

## 목차

1. [**JAVA의 특징**](#1)
2. [**JVM메모리 구조**](#2)
3. [**가비지 컬렉터**](#3)

<br />

<div id="1"></div>

## JAVA의 특징

1. **운영체제 독립적**이다.
   - JAVA는 운영체제나 하드웨어와는 통신하지 않고, JVM과만 통신한다.
   - JVM은 운영체제 종속적이다.
   - JAVA는 한번만 작성되어도 어느 운영체제에서도 사용이 가능하다.
2. **객체 지향 언어**이다.
   - 특징 3가지(상속, 캡슐화, 다형성)
3. **자동 메모리 관리**를 해준다.
   - 가비지 컬렉터가 자동으로 메모리를 관리해준다. (그래서 메모리를 체크,반환하는 일을 해줄 필요가 없다)
4. **네트워크와 분산처리를 지원**한다.
   - 자바는 풍부하고 다양한 표준 라이브러리를 제공한다.
5. **멀티쓰레드를 지원**한다.
   - 관련 라이브러리를 제공한다.(JAVA API)
   - 여러 쓰레드에 대한 스케줄링은 자바 인터프리터가 담당한다.
6. **동적로딩을 지원**한다.
   - 작성한 자바 어플리케이션에 클래스가 여러개여도 모두 로딩하지 않고, 필요할 때마다 로딩하여 사용한다. 그래서 변경사항이 발생하여도 전체 어플리케이션을 다시 컴파일하지 않는다.

<br />

<div id="2"></div>

## JVM의 메모리 구조

### 메소드 영역(method area)

- 사용되는 클래스 파일(\*.class) 정보(클래스 데이터)와 클래스 변수(class variable)가 이곳에 저장됨.
- 클래스,인터페이스,메소드,필드,Static 변수등의 바이트 코드를 보관함.

### 힙 영역(heap)

- 인스턴스가 생성되는 공간
- 가비지 컬렉터가 참조되지 않는 메모리를 확인하고 제거하는 영역

### 호출 스택(call stack,execution stack)

- 메소드 작업에 필요한 메모리 공간을 제공한다.
  - 메소드가 작업을 수행하는 동안 중간의 연산 결과등을 저장하는데 사용됨
- 호출스택의 제일 위에 있는 메소드가 현재 실행중인 메소드이다.
- 그 아래 메소드는 위 메소드를 호출한 메소드이다.

<br />

<div id="3"></div>

## 가비지 컬렉터(Garbage Collector)

Garbage Collection(GC)은 메모리 관리 기법 중 하나로, 프로그램이 동적으로 할당했던 메모리 영역 중에서 필요없게 된 영역을 해제하는 기능으로, 1959년 존 매카시라는 사람이 개발하였다.(wiki)

### JVM-based application’s working cycle

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a5459514-bd82-4e2a-8f5e-e103536123f0/Untitled.png)

- 메모리를 정리하기위해서, 쓰레드가 잠시 멈추는데, 이것을 stop-the-world events 라고 하거나 혹은 STW라고 부른다.
- 가비지 컬렉터가 더이상 사용되어 지지 않는 객체들을 마크한 후, 재요청하면, 이 메모리는 resizing 한다.

> 이 과정에서 핵심은 application threads가 길면 길수록 좋다는 것이다. 그래서, gc를 최소화시켜야 한다. 그래서 generation 개념이 등장하였다.

### Heap의 Generation

Heap 영역은 처음 설계될 때, 2가지를 전제로 설계되었다.

- 객체는 금방 접근 불가능한 상태가 된다.
- 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다.

→ **객체는 대부분 일회성이며, 메모리에 오랫동안 남아있는 경우는 드물다.**

그래서 객체의 생존 기간에 따라서 물리적인 Heap 영역을 나누었는데, Young, Old 2가지 영역이 설계되었다.

- **Young Generation**
  - **Eden space** 와 **Survivor space** 로 나누어진다.
  - 새로운 객체가 할당되는 곳.
  - 대부분의 객체가 이곳에서 사라진다.
  - 여기서 일어나는 GC를 **minor GC**라고 부름
  - 두가지 기술
    - bump-the-pointer
    - TLABs(Thread-Local Allocation Buffers)
- **Old Generation**
  - **Tenured space**
  - 장기간 살아있는 객체가 저장되어진 곳.
  - 여기서 일어나는 GC를 **major GC**라고 부름
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e9a97dd0-9cbb-49a1-869b-254fd06e95a0/Untitled.png)
  생성된 객체는 Eden Space에 가장 먼저 저장이되고, 이후 Survivor Space 0 과 Survivor Space 1으로 차례대로 이동한다. 이 이후까지 살아있는 객체는 Tenured Space로 이동하게 되는데, 이곳이 old generation Space다.
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e04fdefe-07a3-49ba-b188-22af5da1b4b0/Untitled.png)
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e4d62dbc-7787-4e07-a5f0-a00cdde89023/Untitled.png)
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e725b0a-9adf-4b73-b5e0-56f7289cfcb1/Untitled.png)
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a826f878-8706-46be-b7b5-3795d59248e6/Untitled.png)
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/158177bc-5100-43e4-9c83-6c5141865427/Untitled.png)
  > Java 8 이전에는 PermGen (Permanent Generation)이 존재하였음. 클래스나 메소드의 metadata를 저장하는 공간으로, old 영역에서 살아남은 객체가 저장되는 곳( Major GC가 일어남) 하지만, JAVA8 이후에는 Metaspace가 PermGen의 공간을 대체하게 되었다.
  **Metadata Space**
  자동으로 공간이 resized됨.
  Metaspace메모리 공간을 컨트롤하기 위한 몇가지 flag들이 있음.
  - **XX:MetaspaceSize** – initial size of the Metaspace memory region,
  - **XX:MaxMetaspaceSize** – maximum size of the Metaspace memory region,
  - **XX:MinMetaspaceFreeRatio** – minimum percentage of class metadata capacity that should be free after garbage collection,
  - **XX:MaxMetaspaceFreeRatio** – maximum percentage of class metadata capacity that should be free after garbage collection.

JDK7을 기준으로 5가지 방식이 있다.

- Serial GC
- Parallel GC
- Parallel Old GC(Parallel Compacting GC)
- Concurrent Mark & Sweep GC(이하 CMS)
- G1(Garbage First) GC

- **Reference**
  - [https://d2.naver.com/helloworld/1329](https://d2.naver.com/helloworld/1329)
  - [https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html](https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html)
  - [https://sematext.com/blog/java-garbage-collection/#toc-what-is-garbage-collection-in-java-a-definition-0](https://sematext.com/blog/java-garbage-collection/#toc-what-is-garbage-collection-in-java-a-definition-0)
