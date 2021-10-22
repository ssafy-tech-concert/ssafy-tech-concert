<div align="center">
  <br />
  <h1>정렬알고리즘</h1>
  <br />
</div>

## 목차

1. [**버블 정렬**](#1)
2. [**선택 정렬**](#2)
3. [**삽입 정렬**](#3)
4. [**머지 정렬**](#4)
5. [**퀵 정렬**](#5)

<br />

<div id="1"></div>


- **질문 :  수백만개의 숫자중에서 원하는 숫자를 매일 하나씩 찾을 것이다.
매일 수백만개의 숫자중에서 단 하나의 숫자만 바뀐다. 
어떤 알고리즘을 사용할 것인가?**

-------------------

### 1. 버블 정렬 (Bubble Sort)

버블 정렬은 배열에서 2개씩 선택하여 크기를 비교하고 스왑하는 것을 반복한다.
더 좋은 알고리즘들이 많기에 자주 쓰이진 않지만 이해하기가 굉장히 쉬운편임

![](https://images.velog.io/images/alstjdwo1601/post/f88c03be-1a67-46c0-bec7-b7879b4f05cf/image.png)
![](https://images.velog.io/images/alstjdwo1601/post/0af33c12-5872-4eec-83a4-46df84eda790/image.png)
![](https://images.velog.io/images/alstjdwo1601/post/2831fd76-0542-4352-aa3d-4b24bef5fa10/image.png)
![](https://images.velog.io/images/alstjdwo1601/post/1dc26a36-3863-4602-bcdb-d4b6b9099b40/image.png)




- **Time Complexity of Bubble Sort **

(n-1) + (n-2) + .... 2 + 1  -> n(n-1)/2 이므로 O(n^2) 의 시간 복잡도를 가진다 .
중간에 정렬이 완료되었음에도 마지막 회차까지 2개의 원소를 계속 비교하기 때문에 **최선, 평균, 최악의 경우 모두 O(n^2) 의 시간 복잡도를 가진다.**

<hr>
<br />

<div id="2"></div>


### 2. 선택 정렬 (Selection Sort)
![](https://images.velog.io/images/alstjdwo1601/post/426cb7dc-4b35-4d2d-8f64-7ed5e30cf47e/image.png)
1) 전체 아이템 중에서 가장 작은 아이템의 위치를 찾는다
![](https://images.velog.io/images/alstjdwo1601/post/4f129fdd-2619-41cc-96e5-fcb874f75c09/image.png)
2) 가장 첫번째 아이템과 스왑한다.

![](https://images.velog.io/images/alstjdwo1601/post/69dbf787-d206-4273-ac5e-6d73f0b20a8c/image.png)
3) 1은 이제 정렬된 부분이므로 나머지 정렬되지 않은 부분에서 다시 가장 작은 값을 찾는다.

![](https://images.velog.io/images/alstjdwo1601/post/d9e7f47a-7597-4dc8-892e-a54e704a99fa/image.png)
4) 2는 가장 작으면서 가장 앞에 있으므로 스왑하지 않는다.

- **Time Complexity of Selection Sort **

먼저 버블 정렬과 비슷하게 비교와 스왑하는 부분이 있다. 정렬되지 않은 배열에서 가장 작은 숫자를 찾는 것은 N-1 의 비교를 하는 것이다. 하지만 버블정렬과 다르게 항상 N번의 스왑을 하지 않기에 2배정도 빠르다고 알려져 있지만 **최댓값을 배열 전체에서 찾고 O(n) , 그것을 N번 반복하기에 O(n^2) 의 시간 복잡도를 가진다 .**


<br />
<hr>
<div id="3"></div>

### 3. 삽입 정렬 (Insertion Sort)

![](https://images.velog.io/images/alstjdwo1601/post/16757b50-f8ef-4c8d-a114-f02a1029a18c/image.png)
1) 두번째 아이템을 선택 후 왼쪽에 자신보다 큰 값이 있다면 그 값의 앞으로 이동한다.
![](https://images.velog.io/images/alstjdwo1601/post/643ee15e-b3f0-4dc9-93ae-4fad6ddfd855/image.png)
2) 세번째 아이템을 선택 했지만 왼쪽에 자신보다 큰 값이 없으므로 패스

![](https://images.velog.io/images/alstjdwo1601/post/eca941a6-3a21-435b-8b85-62a1dccf6282/image.png)
3) 3을 선택하고 왼쪽에 6을 보면 자신보다 크므로 스왑, 그다음 5도 자신보다 크므로 스왑 2는 자신보다 작으므로 멈춘다.


- **Time Complexity of Insertion Sort **

삽입 정렬은 필요한 아이템만 스캔하기 때문에 선택 정렬, 버블 정렬보다 빠르다. 
그러나, 결국 **시간복잡도는 O(n^2)으로 동일하다**. 결국 최악의 경우엔 가장 작은 값이 맨 뒤쪽에 있으면 맨 앞까지 비교하면서 스왑이 이뤄지기 때문.

#### 하지만 선택 정렬의 경우 이미 정렬이 되어있는데 하나의 값만 삽입해서 다시 정렬하는 경우 O(n) 의 시간복잡도를 가진다는 특징이 있다. 이미 정렬된 경우에는 삽입 정렬이 굉장히 효율적이다.



![](https://images.velog.io/images/alstjdwo1601/post/06c57e79-7ed8-47a8-aa42-e682660aec92/image.png)
<hr>
<br />
<div id="4"></div>


### 4. 머지 정렬 (Merge Sort)


![](https://images.velog.io/images/alstjdwo1601/post/2c4aa79d-0b59-490f-a9ef-b5683b6c77d6/image.png)
1) 먼저 배열을 반씩 계속 나눠서 2개의 값을 가질 때까지 나눈다. (재귀 함수 호출)


![](https://images.velog.io/images/alstjdwo1601/post/4984c12c-0aed-4cd1-b05e-b81f9d811579/image.png)
2) 복사된 2칸 배열에 작은 값을 앞으로 보내서 정렬한다.


![](https://images.velog.io/images/alstjdwo1601/post/f0d45095-86c7-49b5-818f-462162a43dc7/image.png)
3) 정렬된 배열을 다시 원래 배열로 복사한다.

![](https://images.velog.io/images/alstjdwo1601/post/d8c89b56-b466-4f85-ba96-0671461e775b/image.png)
4) 이렇게 모든 파티션을 각각 정렬한다.


![](https://images.velog.io/images/alstjdwo1601/post/d5f04d90-a183-4259-bf67-d4cc06512ff3/image.png)
5) 그럼 이제 앞의 두개의 파티션을 병합한다. 가장 작은 값부터 비교하면서 새로운 배열에 작은값부터 채워 넣는다.

![](https://images.velog.io/images/alstjdwo1601/post/36ce6ffe-aad1-4349-9584-4d09efdd4fed/image.png)

![](https://images.velog.io/images/alstjdwo1601/post/ccf766e2-14cb-4d04-8d7d-53b5a38b85fd/image.png)

![](https://images.velog.io/images/alstjdwo1601/post/c2f046e4-8770-4f28-a97c-fc0345d1afc9/image.png)

![](https://images.velog.io/images/alstjdwo1601/post/8ae3c552-41e1-4141-b98f-559fd39526c8/image.png)


![](https://images.velog.io/images/alstjdwo1601/post/885bdd6a-5dc6-414e-80e5-2eb1b95d1574/image.png)

- **Time Complexity of Merge Sort **

![](https://images.velog.io/images/alstjdwo1601/post/f1c54cdc-a171-47e4-baae-4768926802f8/image.png)

파티션이 낱개가 될때까지 자르므로 N번 재귀함수가 호출되고, 자를 때마다 검색해야하는 데이터 양이 절반씩 줄어드므로 log n 만큼 검색하여** O(nlogn) 의 시간복잡도를 가진다.** 다만 단점으로는 계속 배열을 복사하는 과정에서 메모리를 많이 쓰므로 **공간복잡도가 크다.**


<hr>
<br />
<div id="5"></div>

### 5. 퀵 정렬 (Quick Sort)

![](https://images.velog.io/images/alstjdwo1601/post/d1d08603-9ccb-463e-aa18-9a3547819c82/image.png)
1) 피봇을 골라서 피봇보다 작은건 왼쪽, 큰건 오른쪽으로 옮긴다. 배열의 양 끝에 start , end 포인터를 둔다
start 포인터는 피봇보다 작은 값은 무시하면서 증가하고
end 포인터는 피봇보다 큰 값은 무시하면서 감소한다.

![](https://images.velog.io/images/alstjdwo1601/post/3a265832-134b-4228-92e9-953bcdfc3690/image.png)
2) start 포인터가 가르킨 9가 피봇보다 크므로 멈춘다.


![](https://images.velog.io/images/alstjdwo1601/post/84351ce5-db68-4bd9-8643-6ab8309a8ed3/image.png)
3) end 포인터가 가르키는 2가 피봇보다 작으므로 멈춘다.

![](https://images.velog.io/images/alstjdwo1601/post/45774611-0d2f-4677-b997-ae515f92ff7b/image.png)
4) 두 값을 스왑후 start 와 end 를 다음 값으로 옮기고 반복.

![](https://images.velog.io/images/alstjdwo1601/post/0e7ebcb0-294a-4980-bc5b-e8fb3eb2f50f/image.png)
5) start 는 4를 건너뛰고 7에서 스탑, end 는 8 6 을 건너뛰고 1에서 스탑
그리고 스왑한다.

![](https://images.velog.io/images/alstjdwo1601/post/ee7299a6-0223-481d-81cc-14dcc83098da/image.png)
6) 사이클이 진행되면 피봇보다 작은값들 , 큰값들로 파티션이 나뉨
파티션들에서 다시 피봇을 고르고 퀵소트를 재귀적으로 진행한다.

- **Time Complexity of Quick Sort **
![](https://images.velog.io/images/alstjdwo1601/post/e8448f6f-cdb8-4439-b72a-615d481c24cd/image.png)
1) 피봇을 골라서 피봇보다 작은건 왼쪽, 큰건 오른쪽으로 옮긴다.
즉 피봇이 중간값을 가지면 좋지만 검색해보고 뽑는게 아니므로 배열의 가운데 있는 값을 그냥 고른다. 

![](https://images.velog.io/images/alstjdwo1601/post/90784e19-4daa-4c64-85c9-693009aa8906/image.png)
2) 피봇이 최소값이었기때문에 0을 맨 앞으로 보내고 나머진 다 오른쪽에 둔다.

![](https://images.velog.io/images/alstjdwo1601/post/96be4c6f-68cd-4590-99af-ba5a8d92dfbe/image.png)
3) 왼쪽은 값이 하나라 정렬이 끝났고 오른쪽 파티션에서 다시 피봇을 고른다.
또 피봇이 최소값이었기 때문에 1을 맨 왼쪽으로 고르고 다시 파티션에서 피봇을 고른다.

즉 **피봇이 계속 최소값  or  최대값인 경우엔 최악의 경우이며 이때 O(n^2) 의 시간복잡도를 가지게 된다. 그러나 일반적으로는 O(nlogn)의 시간복잡도를 가진다.**

참고로 **자바에서 우리가 자주쓰는 Arrays.sort() 의 내부 알고리즘은 피봇을 2개 쓰는 Dual Pivot Quick Sort 이다.** 이론적, 실험적으로 랜덤 데이터에 대해 보통 퀵소트보다 상당히 좋은것으로 판명되었으나 역시나 최악의 경우엔 O(n^2)임이 변하진 않는다.

**Collections.sort()의 경우는 삽입정렬 + 머지 정렬인 Tim 정렬을 사용한다고 한다.** 배열은 메모리적으로 각 값들이 연속적 주소를 갖기 때문에 참조 지역성이 좋은 퀵 정렬을 쓰고 Collections.sort()는 보통 어레이리스트뿐 아니라 메모리적으로 산발적인 링크드리스트도 사용하기에 참조 인접성이 좋지 않아서 Tim 정렬을 쓰는것이 평균적으로 더 좋다고 합니다. 


-----------------------

- 질문의 답 :  맨 위에서의 질문의 답은 처음에 값이 수백만개가 있는 값 중에서 원하는 값을 찾기 위해선** 처음에 머지소트나 퀵소트를 활용하여 정렬을 하고 이분 탐색을 하는것이 가장 효율적일 것이다. **
 
 매일 값이 하나 바뀌는 경우에 다시 값을 찾으려면 이분 탐색을 하기위해 매일 정렬을 새로해야하는데 **이미 정렬이 되어 있으므로 삽입 정렬을 해주는 것이 가장 좋을 것이다.**
 
 
 ----------------------------

 [참고한 곳]
 
 유튜브 엔지니어 대한민국 : https://www.youtube.com/user/damazzang <br>
 유튜브 노마드 코더 : https://www.youtube.com/channel/UCUpJs89fSBXNolQGOYKn0YQ
 http://www.secmem.org/blog/2019/05/06/special-sorts-2/
 https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html
https://velog.io/@gillog/%EB%B2%84%EB%B8%94-%EC%A0%95%EB%A0%ACBubble-Sort
https://devuna.tistory.com/28
https://github.com/GimunLee/tech-refrigerator
