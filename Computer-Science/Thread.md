<div align="center">
  <br />
  <h1>Thread</h1>
  <br />
</div>

## 목차

1. [**프로세스와 스레드**](#1)
2. [**멀티 태스킹과 멀티 쓰레딩**](#2)

<br />

<div id="1"></div>

## 프로세스와 스레드

프로그램을 실행하면 OS로부터 실행에 필요한 자원(메모리)을 할당받아 프로세스가 된다.

프로세스 는 실행중인 프로그램으로 실행에 필요한 데이터+메모리+쓰레드로 구성되어 있다.

쓰레드는 실질적으로 자원을 가지고 일을 수행하는 주체를 말한다. 이 스레드는 경량화된 프로세스라고도 하는데, 부모 프로세스의 자원을 이 쓰레드들이 공유자원(코드,데이터,힙 영역)을 사용하고, 각자 stack 영역을 갖는다.

<br />

<div id="2"></div>

## 멀티 태스킹과 멀티 쓰레딩

멀티 태스킹은 여러개의 프로세스를 동시에 실행하는 것

멀티 프로세스

멀티 프로세스

![image](https://user-images.githubusercontent.com/58917737/163188368-3bd92d7f-40bd-42d2-b52b-c8b56fdaaafa.png)

- 프로세스를 fork()하여 동작함

- 프로세스를 fork()하여 동작함
- IPC통신
  - 프로세스는 독립적이다. 그래서 별도의 설비 없이 통신이 어렵다. 그래서 InterProcessCommunication을 제공하여 프로세스간 통신을 할 수 있게 하였다.
  - Method : Anonymous PIPE,Named PIPE,Message Queue,SharedMemory,Message passing,Memory-mapped file,Unix domain socket, Socket...
- Context Switching 비용이 큼
- 동기화 작업이 필요하지 않다.
  - 프로세스가 독립적이기때문에

멀티 쓰레딩은 하나의 프로세스에서 여러개의 쓰레드를 동시에 실행하는 것

![image](https://user-images.githubusercontent.com/58917737/163188468-d6098d3f-6c99-4053-9530-37ad641049b4.png)

- 공유 자원을 사용하여 각자의 Stack을 가지고 동작함
  - 공유 자원을 사용의 장점
    - 통신 비용이 절감됨
    - 메모리가 효율적임
    - Context Switching 비용이 적음
  - 단점
    - 동기화(synchronization)
    - 교착상태(deadlock)

> 테코톡에서 사용한 예시
> Internet Explorer 사용시, 여러 탭을 띄워 작업을 하다가 한 탭이 문제가 생겨 작업이 중지되면, 다른 탭들도 모두 영향을 받아 닫혀버린 경험이 있을 것임
> 왜냐면 쓰레드로 긴밀하게 연결이 되어 있으니까
> Google chrome 사용시, 여러 탭을 띄워 작업을 하다가 한 탭이 문제가 생겨도, 다른 탭들이 영향을 받지 않음
> 왜냐면 프로세스로, 조금 비효율적일지라도, 각자도생을 하기때문

### CPU ( 코어)는 한번에 하나씩의 일만 처리할 수 있다.

컨텍스트 스위칭을 통해서 작업이 동시에 일어나는 것처럼

여기서, CPU(core)는 한번에 하나씩의 일만을 처리할 수 있기 때문에, 여러개의 일을 동시에 처리하는 것처럼 보이게하기 위해서 번갈아가면서 일을 처리한다. 그래서 쓰레딩의 개수와 성능이 비례하지 않는다.

### 그러면 병렬처리가 뭐야 그건 동시에 하는거 아닌가?

멀티코어는 한번에 하나씩만 일을 처리할 수 있는 이 코어가 여러개 있다는 말이다. 그래서 코어마다 여러 개의 작업을 나누어 배분하는 병렬처리가 가능하다.

멀티 태스킹을 하게되면, 싱글 코어에서는 병행적으로 처리한다. (번갈아가면서)

하지만 멀티 코어에서는 스레드가 각 코어로 배분되어 병렬적으로 처리가 가능하다.

<br />

## Reference

- 자바의 정석
- [[10분 테코톡] 코다의 Process vs Thread](https://www.youtube.com/watch?v=1grtWKqTn50)
- [https://you9010.tistory.com/136](https://you9010.tistory.com/136)