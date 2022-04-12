<div align="center">
  <br />
  <h1>프론트엔드에서 클린 코드 짜기</h1>
  <br />
</div>

## 목차

1. [**클린 코드**](#1)
2. [**클린 코드를 짜기 위해 신경쓰기**](#2)
3. [**실무에서 클린 코드**](#3)
4. [**클린 코드를 짜기 위한 마음 가짐**](#4)

<br />

<div id="1"></div>

## 클린 코드

### 실무에서 클린 코드의 의의

- 클린 코드는 짧은 코드가 아니고 **원하는 로직을 빠르게 찾을 수 있는 코드**
- 클린 코드의 반대 : 흐름 파악이 어렵고 도메인 맥락 표현이 안 되어 동료에게 물어봐야 알 수 있는 코드 ⇒ `아, 그 코드 그냥 제가 수정할게요`
- 클린 코드의 장점 : **유지보수 시간의 단축**
  - 코드 파악, 디버깅, 리뷰에 투자하는 시간 감소
  - 시간 = 자원 = 돈

### 클린 코드의 반대 상황

- 처음에는 클린한 코드지만, 해당 코드에 기능을 덕지덕지 추가하게 되면서 복잡해진다
  ⇒ 안일한 코드 추가의 함정
- 동일한 기능을 하는 코드가 여러군데 흩어져있다
- 하나의 함수가 여러 가지 일을 하고 있다

<br />

<div id="2"></div>

## 클린 코드를 짜기 위해 신경쓰기

- 원하는 로직만 찾으려면?
  - 하나의 목적을 가진 코드가 흩뿌려져 있다면 ⇒ **하나로 묶어 응집도를 높이자**
  - 함수가 여러 가지 일을 하고 있다면 ⇒ **단일책임 원칙에 의거하여 각각 쪼개주자**
  - 함수의 세부구현 단계가 제각각이라면 ⇒ **추상화 단계를 조정해서 핵심 기능을 필요한 기능만큼 유출하자**

### 응집도

- 하나의 목적을 가진 코드가 흩뿌려져 있다면 하나로 묶어놓자
- 모두 묶을 필요는 없다

  - 당장 몰라도 되는 디테일 ⇒ `뭉쳐놓기`
  - 코드 파악에 필수적인 핵심 정보 ⇒ `풀어놓기` (여러 모듈을 넘나들면서 찾아야하기 때문)

- **선언적 프로그래밍**

  - 무엇을 하는 함수인지 빠르게 파악 가능
  - 세부 구현은 안쪽에 뭉쳐두었기 때문에 신경 쓸 필요가 없다
  - 무엇만 바꾸어 쉽게 재사용할 수 있다
    ```javscript
    <Popup
        onSubmit={질문전송}
        onSuccess={홈으로 이동}
    />
    ```

- **명령형 프로그래밍**

  - 어떻게 해야할지 하나하나 명령하기

    - 커스텀이 쉽다
    - 읽기 오래 걸리고 재사용하기 어렵다

    - 선언적 프로그래밍도 내부까지 포함하면 명령형 프로그래밍으로 작성되어 있다

    ```javscript
    <Popup>
        <button oncClick={
            async () => {
                const res = await 질문전송();
                if(res.success) {
                    홈으로이동();
                }
        }}>전송</button>
    </Popup>
    ```

- **결론 : 선언적인 코드와 명령적 코드를 둘 다 유동적으로 섞어서 사용할 것**

### 단일 책임

- **함수가 여러 가지 일을 하고 있다면 각각 쪼개주자**
- 하나의 일을 하는 뚜렷한 이름의 함수를 만들자
- 예시

  - 문제되는 코드

    - 이때 handle질문제출이 이름이라면 약관 체크 후 팝업이라는 포인트가 빠져있기 때문에 코드 신뢰가 하락한다 ⇒ 함수명을 믿지 못하고 함수를 모두 확인하는 상황 발생
    - 기능이 추가되면 더 복잡해진다
    - 약관 동의를 받은 뒤 질문을 전송 ⇒ 해당 질문에 대한 연결전문가가 존재할 경우 해당 전문가에게 질문 전송하기

    ```javscript
    async function handle질문제출() {
        const 약관동의 = await 약관동의_받아오기(); // 약관 체크 후 팝업
        if (!약관동의) {
            await 약관동의_팝업열기();
        }
        await 질문전송(questionValue); // 질문 제출
        alert('질문이 등록되었어요');

        // 이후에 기능이 추가되면서 아래 코드 추가
        const 연결전문가 = await 연결전문가_받아오기(); // 연결전문가 질문 전송
        if (연결전문가 !== null) {
            await 연결전문가_질문전송(qeustionValue);
            alert(`${연결전문가.name}에게 질문이 등록되었어요`);
        }
    }
    ```

  - 리팩토링된 코드

    - 한 가지 일만 하는 명확한 이름의 함수

    ```javscript
      async function handle연결전문가질문제출() {
          await 연결전문가_질문전송(questionValue);
          alert(`${연결전문가.name}에게 질문이 등록되었어요`);
      }
      async function handle새전문가질문제출() {
          await 질문전송(questionValue); // 질문 제출
          alert('질문이 등록되었어요');
      }
      async function handle약관동의팝업열기() {
          const 약관동의 = await 약관동의_받아오기(); // 약관 체크 후 팝업
          if (!약관동의) {
              await 약관동의_팝업열기();
          }
      }
    ```

- 한가지 일만 하는 기능성 컴포넌트 예시

  - 문제되는 경우

    - 버튼 클릭 함수에 로그 찍는 함수와 API 콜이 섞여 있다

    ```javscript
    <button
        onClick = { async () => {
            log('제출 버튼 클릭')
            await openConfirm();
        }}
    />
    ```

  - 리팩토링된 코드

    - 로그는 버튼을 감싼 컴포넌트에서 찍고, 버튼 클릭함수에서는 API 콜만 신경쓴다

    ```javscript
    <LogClick message='제출 버튼 클릭'>
        <button onClick={openConfirm} />
    </LogClick>
    ```

- 팁 : 한글 변수명을 사용하기

  ```javscript
  const 패널티풀림 = reasons.indexOf('PENALTY') > -1;
  const 평점4점이상 = review.rate >= 80;

  if (패널티풀림) {
      return //
  }
  if (평점4점이상) {
      return //
  }
  ```

  ```javscript
  const 패널티풀림 = reasons.indexOf('PENALTY') > -1;
  const 평점4점이상 = review.rate >= 80;

  if (패널티풀림) {
      return //
  }
  if (평점4점이상) {
      return //
  }
  ```

### 추상화

- **함수의 세부구현 단계가 제각각이라면 로직에서 핵심 개념을 뽑아내자**
- 컴포넌트 예시

  - 팝업 코드를 밑바닥부터 구현

    ```javscript
    <div style={팝업스타일}>
        <button oncClick={
            async () => {
                const res = await 질문전송();
                if(res.success) {
                    홈으로이동();
                }
        }}>전송</button>
    </div>
    ```

  - 중요 개념만 남기고 추상화

    ```javscript
    <Popup
        onSubmit={질문전송}
        onSuccess={홈으로 이동}
    />
    ```

- 함수 예시

  - 전문가 정보를 받아와서 응답 값에 따라 다른 정보 보여주기
  - 설계사 라벨을 얻는 코드 세부 구현

    ```javscript
    const planner = await fetchPlanner(plannerId);
    const label = planner.new ? '새로운 상담사' : '연결중인 상담사';
    ```

  - 중요 개념을 함수 이름에 담아 추상화

    ```javscript
    const label = await getPlannerLabel(plannerId);
    ```

- 얼마나 추상화할 것인가?

  - **Level 0**

    - Confirm 버튼을 클릭하면 특정 메시지 띄우기

    ```javscript
    <Button onClick={showConfirm}>
        전송
    </Button>
    {isShowConfirm && (
        <Confirm onClick={() => {showMessage('성공')}} />
    )}
    ```

  - **Level 1**

    - 버튼 클릭시 컨펌 창 띄우는 기능을 ConfirmButton으로 추상화

    ```javscript
    <ConfirmButton
        onConfirm={() => {showMessage('성공')}}>
        전송
    </ConfirmButton>
    ```

  - **Level 2**

    - message라는 props만 넘겨서 컨펌 창에 내가 원하는 메세지만 보여주기

    ```javscript
    <ConfirmButton message="성공">
        전송
    </ConfirmButton>
    ```

  - **Level 3**

    - 모든 기능을 그냥 ConfirmButton에 추상화하기

    ```javscript
    <ConfirmButton />
    ```

  - **답은 없다 ⇒ 상황에 따라 필요한만큼만 추상화하면 된다**

  <br />

<div id="3"></div>

## 실무에서 클린 코드

- 추상화할 수 있을까요?
- 추상화를 깬 이유 설명 ⇒ 중복이 심하지 않아 유연성을 위해 깼다
- 추상화 수준을 맞추자
  - 추상화 단계가 섞여 있는 경우
    - 추상화 수준이 섞여있다면 전체적인 코드가 어느 수준으로 구체적으로 기술된지 파악할 수 없다
    - 중간 추상화된 컴포넌트 코드를 보고 높은 추상화 컴포넌트 또한 구체적으로 작성되었다고 생각할 수 있음 ⇒ 실제로 보기 전까지는 알 수 없음
    ```javscript
    <Title>별점을 매겨주세요</Title> {/_ 높은 추상화 _/}
    <div> {/* 낮은 추상화 */}
        {STARS.map(() => <Star />)}
    </div>
    <Reviews /> {/* 높은 추상화 */}
    {rating !== 0 && ( {/* 중간 추상화 */}
        <>
            <Argreement />
            <Button rating={rating} />
        </>
    )}
    ```
  - 추상화 단계가 맞춰진 경우 ⇒ 쉽게 파악 가능
    ```javscript
    <Title>별점을 매겨주세요</Title>
    <Stars />
    <Reviews />
    <ArgreementButton
        show={rating !== 0}
    />
    ```

<br />

<div id="4"></div>

## 클린 코드를 짜기 위한 마음 가짐

- 담대하게 기존 코드 수정하기
  - 두려워하지 말고 기존 코드를 씹고 뜯고 맛보고 즐기자
- 큰 그림 보는 연습하기
  - 기능 추가 자체는 클린해도 전체적으로는 어지러울 수 있다
- 팀과 함께 공감대 형성하기
  - 코드에 정답은 없으니 명시적으로 이야기 하는 시간을 가지자
  - 어떻게 개선할지 함께 고민하자
- 문서로 적어보기
  - 글로 적어야 명확해진다
  - 향후 어떤 점에서 위험할 수 있는지, 어떻게 개선할 수 있는지 생각하자

<br />
<br />

###### 출처: [토스ㅣSLASH 21 - 실무에서 바로 쓰는 Frontend Clean Code](https://www.youtube.com/watch?v=edWbHp_k_9Y)

<br />
<br />
