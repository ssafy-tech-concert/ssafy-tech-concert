<div align="center">
  <br />
  <h1>인덱스는 왜 대부분 B-Tree를 선택했을까</h1>
  <br />
</div>

## 목차

1. [**인덱스란?**](#1)
2. [**왜 B-tree?**](#2)
3. [**다른 밸런스 트리는?**](#3)
4. [**그럼 배열은?**](#4)
5. [**탐색시간 제일 빠른 Hash Table은?**](#5)
6. [**결론**](#6)

<br />

<div id="1"></div>

## 인덱스란?
[https://github.com/ssafy-tech-concert/ssafy-tech-concert/blob/master/Back-end/index.md](https://github.com/ssafy-tech-concert/ssafy-tech-concert/blob/master/Back-end/index.md)

![image](https://user-images.githubusercontent.com/56222478/161429466-15c9356f-f782-480b-ae31-18303d5188f1.png)


<br />

<div id="2"></div>

## 왜 B-tree?

**Average case of Tree algorithm**

<img src="https://blog.kakaocdn.net/dn/8G0vu/btqLD1UBlSK/M7CFNHdOCfIbR9HWtOjFsk/img.png" width="400" height="300">

Tree는 평균적으로 탐색에 대한 시간 복잡도로 O(logN)을 가진다.

**Worst case of Tree algorithm**

<img src="https://blog.kakaocdn.net/dn/bzgf6i/btqLGXpGgsh/DX53GJSepCN3K5jcx5nKU1/img.png" width="400" height="400">

최악의 경우 탐색 시간은 O(N)을 가지게 된다.

이러한 경우를 방지하기 위해 우리는 밸런스 트리(Balanced Tree)를 이용할 수 있다.

- ***밸런스 트리(Balanced Tree)란?***
    
    트리의 노드가 한 방향으로 쏠리지 않도록 노드 삽입 및 삭제 시 특정 규칙에 맞게 재정렬되어 왼쪽과 오른쪽 자식 양쪽 수의 밸런스를 유지하는 트리이다.
    
    항상 양쪽 자식의 밸런스를 유지하므로 무조건 O(logN)의 시간 복잡도를 가지게 된다.
    
    하지만, 노드 삽입 및 삭제 시 발생하는 재정렬 작업 때문에 탐색을 제외한 작업에서는 일반 Tree보다 성능이 좋지 않다.
    

밸런스 트리는 최악의 경우에도 탐색에 대한 시간 복잡도가 O(logN)이므로, 탐색시간에 매우 효율적인 자료구조이다.

그래서 데이터베이스의 인덱스는 밸런스 트리, 그중 B-Tree를 선택했다.

<br />

<div id="3"></div>

## 다른 밸런스 트리는?

![image](https://user-images.githubusercontent.com/56222478/161429501-39af2ef7-1008-4a31-9c25-40315d7a82e8.png)

위 두 개의 트리는 항상 좌, 우 자식노드 개수의 밸런스를 유지하므로 최악의 경우에도 탐색 시간이 O(logN)을 가지게 된다.

그렇다면 B-Tree 뿐 아니라, RedBlack-Tree도 DB 인덱스로 사용해도 괜찮지않을까?

**RedBlack-Tree와 B-Tree의 차이는 무엇일까?**

이 둘의 가장 큰 차이는 '하나의 노드가 가지는 데이터 개수'이다.

RedBlack-Tree는 무조건 하나의 노드에 하나의 데이터 요소만을, B-Tree는 하나의 노드에 여러 개의 데이터 요소를 저장한다.

![https://blog.kakaocdn.net/dn/dxEzhq/btqLD18oVdY/panRlOS99wVghfZUlxKDV0/img.png](https://blog.kakaocdn.net/dn/dxEzhq/btqLD18oVdY/panRlOS99wVghfZUlxKDV0/img.png)

하나의 노드 내의 데이터들은 **항상 정렬된 상태를 유지하며 마치** "**배열**"의 모습을 띄고 있는데

실제 메모리 상에 배열처럼 차례대로 저장이 되어있다.

**때문에 같은 노드 공간의 데이터를 탐색할 때는 포인터 접근을 하는 것이 아니라 실제 메모리 디스크에서 바로 다음 인덱스의 접근을 할 수 있다.**

![https://blog.kakaocdn.net/dn/bCQmcS/btqLEN2Wdk8/mx7mIKwVLR7UpPbPyb2zS0/img.png](https://blog.kakaocdn.net/dn/bCQmcS/btqLEN2Wdk8/mx7mIKwVLR7UpPbPyb2zS0/img.png)

RedBlack-Tree는 B-Tree와 다르게 **각 노드마다 무조건 하나의 데이터만 가지게 되므로 모든 데이터를 접근할 때 무조건 참조 포인터로 접근을 하게 된다.**

**따라서 둘 다 시간 복잡도는 O(logN)이지만 이러한 시간 복잡도는 알고리즘 처리에 대한 이론적인 시간 계산 방식일 뿐 물리적인 시간 개념으로는 B-Tree의 배열 형식의 접근과 RedBlack-Tree의 참조 포인터 접근의 시간 차이가 생긴다.**

포인터로 메모리에 접근 시 CPU 연산을 통해 주소를 알아내는 등의 부가적인 연산이 필요하기 때문에 실제 메모리 디스크에서 바로 다음 인덱스로 접근을 하는 배열 방식이 포인터 접근을 하는 것보다 훨씬 빠를 수밖에 없다.

**비록 같은 O(logN)이지만, 포인터 접근 수의 차이로 인해 B-Tree가 RedBlack-Tree보다 탐색 시간이 더 빠를 수밖에 없다.**

<br />

<div id="4"></div>

## 그럼 배열은?

배열은 참조 포인터라는 개념이 없고, 모든 데이터가 메모리 상 차례대로 저장되어 있으므로 배열의 인덱스를 통해 O(1)의 시간 복잡도로 요소를 조회할 수 있다.

참조가 없으니 당연히 탐색 속도로는 B-Tree보다 훨씬 빠르다.

하지만 배열에서 빠른 것은 "**탐색**"뿐이다.

<img src="https://blog.kakaocdn.net/dn/cAXjfM/btq6LWX732C/s6UylXHe2BZ31xhf9jmPQk/img.png" width="600" height="400">

삽입 및 삭제 시에는 기존 데이터들을 이동하는 시간이 걸려서 평균적으로 O(N)이 걸린다.

참고로 B-tree의 삽입, 삭제는 트리의 높이(h)에 따른 O(h)의 시간 복잡도를 가지는데, 이는 logN보다 훨씬 작은 값이다.

<br />

<div id="5"></div>

## 탐색시간 제일 빠른 Hash Table은?

<img src="https://blog.kakaocdn.net/dn/cSdWcV/btqLDOnT21u/cYdqhhPUIm1KgBIt3hWVt0/img.png" width="600" height="400">

Hash Table의 평균 탐색 시간 복잡도는 O(1)로 매우 빠르다.

그러나 이는 '*단 하나의 데이터를 탐색하는 경우'* 에만 O(1)이다.

DB는 등호(=) 연산 뿐 아니라 부등호(<, >) 연산도 사용하는데, Hash Table에 저장되는 값들은 정렬되어 있지 않기 때문에 특정 값보다 크거나 작은 값을 찾을 수 없다.

찾을 수 있다 하더라도 O(1)의 시간 복잡도를 보장할 수 없고 매우 비효율적이다.

이로한 이유로 Index 자료 구조로 해시 테이블을 사용하는 경우는 매우 제한적이다.

<br />

<div id="6"></div>

## 결론

1. **항상 정렬된 상태로 특정 값보다 크고 작은 부등호 연산에 문제가 없다.**
2. **참조 포인터가 적어 방대한 데이터 양에도 빠른 메모리 접근이 가능하다.**
3. **데이터 탐색뿐 아니라, 저장, 수정, 삭제에도 항상 O(logN)의 시간 복잡도를 가진다.**
