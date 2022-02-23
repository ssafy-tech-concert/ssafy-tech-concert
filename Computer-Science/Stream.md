<div align="center">

<br />

<h1>스트림(Stream) 소개</h1>

<br />

</div>

## 목차

1. [**기존 방식의 문제점들**](#1)

2. [**스트림의 특징**](#2)

3. [**스트림의 연산**](#3)

4. [**Stream<T>와 IntStream,LongStream,DoubleStream**](#4)

<br />

<div id="1"></div>

## 기존 방식의 문제점들

1. 재사용성이 떨어지고 코드가 길어짐(for 문, Iterator)
2. 데이터 소스마다 다른 방식으로 다뤄야함 (ex, Collections.sort(),Arrays.sort()..)

→ 스트림(Stream)은 이 방식들을 해결하였다.

**스트림은 데이터 소스를 추상화 하였고, 메서드들이 같은 방식으로 다룰 수 있게 되어 있다.**

<br />

<div id="2"></div>

## 스트림의 특징

1. **스트림은 데이터 소스를 변경하지 않는다.**

   → 스트림은 데이터 소스로부터 데이터를 소비하는 것이지, 데이터 소스를 변경하지 않는다.

2. **스트림은 일회용이다.**

   ```java
   IntStream stream = IntStream.of(1,2,3,4);
   stream.forEach(System.out::println);

   stream.forEach(System.out::println); //IllegalStateException이 발생함
   ```

3. **스트림은 작업을 내부 반복으로 처리한다.**

   → 컬렉션 같은 경우 외부 반복이므로, 사용자가 for-each등을 사용하여 반복을 시켜야 한다.

   → 내부 반복을 사용하게 되면, 병렬로 처리하거나, 최적화 순서로 처리를 할 수 있는 장점이 있다. 반면, 외부적으로 반복하면 최적화를 달성하기가 힘들다.

   → 스트림 라이브러리의 내부 반복은 데이터 표현과 하드웨어를 활용한 병렬성 구현을 자동으로 선택한다.

   → ~~반복문은 기본적으로 변수 초기화와 종료 여부를 확인하므로, “오버헤드 횟수”가 내부 반복의 시간 단축의 원인일 수 있다.~~

4. 스트림은 간단하게 병렬처리가 가능하다. (Fork&Join 프레임워크 사용)

   → 멀티 코어의 수만큼 대용량 요소들을 서브 요소들로 나누고, 각각의 서브 요소들을 분리된 스레드에서 병렬처리한다.

   → Thread에 대해 공부 후, 내용 추가 필요

   → threadPool을 공용으로 사용하기 때문에, 모든 병렬 Stream이 동일한 ThreadPool에서 thread를 가져와 사용하여 문제점이 생길 수 있다.

   → Thread가 모두 점유중일 경우, Thread Pool Queue에 쌓이게 되고, 일정치 이상 쌓일경우, 요청이 drop될 수도 있기 때문에 좋지 않다.

   → 커스텀 ForkJoinPool을 사용하여 이를 해결할 수 있다.

   ```java
   strStream.parallel() //이 방법으로 간단하게 병렬 스트림으로 전환 가능
   strStream.sequential() // 병렬 처리를 하지 않게 함
   											 // 스트림은 기본적으로 병렬 스트림이 아니므로, 많이 필요하지는 않음
   ```

<br />

<div id="3"></div>

## 스트림의 연산

<aside>
💡 최종연산이 수행되기 전까지 중간 연산이 수행되지 않는다.

</aside>

스트림에 대하여 distinct()나 sort()같은 중간 연산을 호출해도 즉각적인 연산이 수행되는 것이 아니다. 이는 단지 어떤 작업이 수행되어야 하는지 지정해주는 것 뿐이다.

- 중간 연산
  - 연산 결과가 스트림으로 반환된다.
  - 종류
    | 종류 | 설명 |
    | ------------------------------------------ | ----------------------- |
    | Stream<T> distinct() | 중복 제거 |
    | Stream<T> filter(Predicate<T> predicate) | 조건에 안맞는 요소 제거 |
    | Stream<T> limit(long maxSize) | 스트림 일부 잘라냄 |
    | Stream<T> skip(long n) | 스트림 일부 건너뜀 |
    | Stream<T> peek(Consumer<T> action) | 스트림 요소 작업 수행 |
    | Stream<T> sorted() |
    | Stream<T> sorted(Comparator<T> comparator) | 스트림의 요소 정렬 |
    | Stream<R> map(Function<T,R> mapper) |
    DoubleStream mapToDouble(ToDoubleFunction<T> mapper)
    IntStream mapToInt(ToIntFunction<T> mapper)
    LongStream mapToLong(ToLongFunction<T> mapper)
    Stream<R> flatMap(Function<T,Stream<R>> mapper
    DoubleStream flatMapToDouble (Function<T,DoubleStream> m)
    IntStream flatMapToInt(Function<T,IntStream> m)
    LongStream flatMapToLong(Function<T,LongStream> m) | 스트림 요소 변환 |
- 최종 연산
  - 연산 결과가 스트림이 아닌 연산으로 스트림 요소를 소모하므로, 단 한번만 가능하다.
  - 종류
    | 최종 연산 | 설명 |
    | --------------------------------------------------- | ----------------------- |
    | void forEach(Consumer<? super T> action) |
    | void forEachOrdered (Consumer<? super T> action | 요소에 지정된 작업 수행 |
    | long count() | 요소 개수 반환 |
    | Optional<T> max (Comparator<? super T> comparator) |
    | Optional<T> min(Comparator<? super T> comparator) | 최대값,최소값 |
    | Optional<T> findAny() |
    | Optional<T> findFirst() | 스트림 내 요소 하나 |
    | boolean allMatch(Predicate<T> p) // 모두 만족하는지 |
    boolean anyMatch(Predicate<T> p) // 하나라도 만족하는지
    boolean noneMatch(Predicate<> p)// 모두 만족하지 않는지 | 모든 요소가 만족하는지, 아닌지 확인 |
    | Object[] to Array()
    A[] toArray(IntFunction<A[]> generator) | 스트림의 모든 요소를 배열로 반환 |
    | Optional<T> reduce (BinaryOperator<T> accumulator)
    T reduce (T identity, BinaryOperator<T> accumulator)
    U redduce (U identity, BiFunction<U,T,U> accumulator, BinaryOperator<U> combiner | 요소를 하나씩 줄여가면서 계산 |
    | R collect(Collector<T,A,R> colloector)
    R Collector (supplier<T> supplier,BiConsumer<R,T> accumulator, BiConsumer<R,R> combiner | 스트림 요소를 수집, 그 요소를 그룹화하거나 분할한 결과를 컬렉션에 담아 반환하는데 사용함 |

<div id="4"></div>

## Stream<T>와 IntStream,LongStream,DoubleStream

Stream<T>의 경우 연산 과정이 비효율적이다. (오토박싱 & 언박싱)

IntStream,LongStream,DoubleStream을 사용하는 것이 더 좋다.

- **오토박싱&언박싱**
  오토박싱& 언박싱으로 자바 컴파일러가 변환시켜 주지만, 이는 내부적으로 추가 연산 작업이 필요하기 때문에, 동일한 타입 연산이 이루어지도록 구현하는 것이 좋다.

## Reference

- [https://velog.io/@adam2/JAVA8의-스트림-알아보기](https://velog.io/@adam2/JAVA8%EC%9D%98-%EC%8A%A4%ED%8A%B8%EB%A6%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)
- [https://sabarada.tistory.com/102](https://sabarada.tistory.com/102)
- [자바의 정석](https://book.interpark.com/product/BookDisplay.do?_method=detail&sc.prdNo=249927409&gclid=Cj0KCQiA09eQBhCxARIsAAYRiykE-OXreE6Ow2Psan6xGEd3G31b2wrV5Wa6_MP9VbRT8R9yZhYsXyoaAv9GEALw_wcB)
