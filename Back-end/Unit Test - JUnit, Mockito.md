<div align = "center">
    <br / >
    <h1>
        단위 테스트 - JUnit, Mockito
    </h1>
    <br />
</div>

## 목차

1. [**단위 테스트란?**](#1)
2. [**JUnit**](#2)
3. [**Mockito**](#3)



<br />

<div id="1"></div>

## 1. 단위 테스트(Unit Test)란?

<br />
<br />



### 단위 테스트 vs 통합 테스트

<br />

**[단위 테스트]**

하나의 "모듈"을 기준으로 독립적으로 진행되는 가장 작은 단위의 테스트

- 모듈 : 애플리케이션에서 작동하는 **하나의 기능 또는 메소드**

<br />

**[통합 테스트]**

모듈을 통합하는 과정에서 모듈 간의 호환성을 확인하기 위해 수행되는 테스트

👉 웹 페이지로부터 API를 호출하여 어플리케이션이 올바르게 동작하는지를 확인하는 테스트

<br />
<br />

### 단위 테스트의 장점

통합 테스트에 비해,

- 테스팅에 대한 시간과 비용을 절감할 수 있다.
- 새로운 기능 추가 시에 수시로 빠르게 테스트가 가능하며, 문제도 빠르게 파악할 수 있다.

+) TDD에서의 테스트도 '단위 테스트'를 의미

<br />
<br />

### Stub

- 1개의 모듈이 동작하기 위해 다른 객체들과 메세지를 주고 받아야 하는 경우 多

  → 단위 테스트는 독립적인 테스트이므로 문제 발생

👉다른 객체 대신에 가짜 객체(Mock Object)를 주입하여 어떤 결과를 반환하라고 정해진 답변을 준비시키는 **stub** 사용

<br />

ex) DB에 insert를 테스트한다고 하면, 가짜 DB를 주입해 insert 처리 시에 반드시 1을 반환하도록 함

<br />
<br />

### 좋고 깨끗한 테스트 코드란?

: 1개의 테스트 함수에 대해 assert를 최소화 하고, 1가지 개념만을 테스트해야 함



Clean Code 책에 의하면, FIRST라는 규칙을 따라야 함.

1. Fast : 테스트는 빠르게 동작하여 자주 돌릴 수 있어야 한다.
2. Independent : 각각의 테스트는 독립적이며 서로 의존해서는 안된다.
3. Repeatable : 어느 환경에서도 반복 가능해야 한다.
4. Self - Validating : 테스트는 성공 또는 실패로 bool 값으로 결과를 내어 자체적으로 검증되어야 한다.
5. Timely : 테스트는 적시에 즉, 테스트하려는 실제 코드를 구현하기 직전에 구현해야 한다.



<br />

<br />

<div id="2"></div>

## 2. JUnit

<img src="../images/JUnit.jpg" width="300">



```
순수 JAVA 애플리케이션에 대한 단위테스트 도구
```

2가지 라이브러리 사용

- JUnit5 : 자바 단위 테스트를 위한 테스팅 프레임워크
- AssertJ : 자바 테스트를 돕기 위해 다양한 문법을 지원. 가독성을 향상시켜 줌

<br />

**[ given / when / then 패턴]**

- given(준비) : 어떠한 데이터가 준비되었을 때
- when(실행) : 어떠한 함수를 실행하면
- then(검증) : 어떠한 결과가 나와야 한다.


<br />
<br />
### 단위 테스트 작성 예시

<br />

**[로또 생성기 Java 코드]**

2000원을 주면 1에서 45까지의 수 중 6개를 랜덤으로 골라서 로또를 생성해주는 클래스 정의

```java
public class LottoNumberGenerator{
    
    public List<Integer> generate(final int money){
        if(!validMoney(money)){
            throw new RuntimeException("올바른 금액이 아닙니다!");
        }
        return generate();
    }
    
    private boolean validMoney(final int money){
        return money == 2000;
    }
    
    private List<Integer> generate(){
        return new Random().ints(1, 45 + 1).limit(6)
            .distinct().boxed()
            .collect(Collectors.toList());
    }
}
```

- distinct() : 중복 객체를 제거
- boxed() : 기본형 타입(int, double..)을 참조형(Integer, Double...)요소로 박싱해서 스트림 생성

<br />
<br />

**[1. 로또 번호 갯수 테스트]**

```java
@DisplayName("로또 번호 갯수 테스트")
@Test
void lottoNumberSizeTest(){
    //given
    final LottoNumberGenerator lottoNumberGenerator = new LottoNumberGenerator();
    final int price = 2000;
    
    //when
    final List<Integer> lotto = lottoNumberGenerator.generate(price);
    
    //then
    assertThat(lotto.size()).isEqualTo(6);
}
```

- @Test : 해당 메소드가 단위 테스트임을 명시해 Junit이 단위 테스트로 인식하여 실행시키게 함
- @DisplayName() : 테스트 이름을 default 말고 원하는 이름으로 명시 

<br />

<br />

**[2. 로또 번호 범위 테스트]**

```java
@DisplayName("로또 번호 범위 테스트")
@Test
void lottoNumberRangeTest(){
    //given
    final LootoNumberGenerator lottoNumberGenerator = new LottoNumberGenerator();
    final int price = 2000;
    
    //when
    final List<Integer> lotto = lottoNumberGenerator.generate(price);
    
    //then
    assertThat(lotto.stream().allMatch(v -> v >=1 && v <= 45)).isTrue();
}
```

- isTrue() 외에도 isFalse(), isNull(), isNotNull() 등의 메소드가 있음

<br />

<br />

**[3. 잘못된 로또 금액 테스트]**

잘못된 금액이 발생한 경우, 예외가 잘 발생하는지에 대한 테스트

👉 실패 테스트까지 작성해야 함.

```java
@DisplayName("잘못된 로또 금액 테스트")
@Test
void lottoNumberInvalidMoneyTest(){
    //given
    final LootoNumberGenerator lottoNumberGenerator = new LottoNumberGenerator();
    final int price = 5000;
    
    //when
    final RuntimeException exception 
        = assertThrows(RuntimeException.class,
                       () -> lottoNumberGenerator.generate(price));
    
    //when
    assertThat(exception.getMessage()).isEqualTo("올바른 금액이 아닙니다!");
   
}
```

<br />

일반적인 웹 애플리케이션은 상당히 복잡하고, 여러 객체들 간에 의존성이 있으며 서로 메세지를 주고받음

👉 Spring 기반의 애플리케이션에 대한 단위 테스트는 **Mockito** 사용



<br />

<br />

<br />

<div id="3"></div>

## 3. Mockito

<img src="../images/mockito.png">



```
개발자가 동작을 직접 제어할 수 있는 가짜(Mock)객체를 지원하는 테스트 프레임워크
👉 가짜 객체에 원하는 결과를 Stub 하여 단위 테스트 진행 가능
```

<br />

### Mockito 사용법

<br />

**어노테이션**

- @Mock : Mock 객체를 만들어 반환해주는 어노테이션
- @InjectMocks : @Mock으로 생성된 가짜 객체를 자동으로 주입시켜 줌

<br />

**stub 메소드**

- doReturn() : Mock 객체가 특정한 값을 반환해야 하는 경우
- doNothing() : Mock 객체가 아무 것도 반환하지 않는 경우
- doThrow() : Mock 객체가 예외를 발생시키는 경우

<br />

ex) UserService의 findAllUser() 호출 시에 빈 ArrayList를 반환해야 한다면,

doReturn(new ArrayList()).when(userService).findAllUser();

<br />

<br />

### Spring 컨트롤러 단위 테스트 작성 예시

**[사용자 회원가입/목록 조회 API]**

```java
@RestController
@RequiredArgsConstructor
public class UserController{
    private final UserService userSerivce;
    
    @PostMapping("/user/signUp")
    public ResponseEntity<String> signUp(@RequestBody final SignUpDTO signUpDTO){
        return userService.isEmailDuplicated(signUpDTO.getEmail())
            ? ResponseEntity.badReqeust().build()
            : ResponseEntity.ok(TokenUtils.generateJwtToken(userService.signUp(signupDTO)));
    }
    
    @GetMapping("/user/list")
    public ResponseEntity<UserListResponseDTO> findAll(){
        final UserListResponseDTO userListResponseDTO = UserListResponseDTO.builder()
            .userList(userService.findAll()).build();
        
        return ResponseEntity.ok(userListResponseDTO);
    }
}
```

<br />

<br />

**[단위 테스트 작성 준비]**

```java
@ExtendsWith(MockitoExtenstion.class)
class UserControllerTest{
	
    @InjectMocks
    private UserController userController;
    
    @Mock
    private UserService userSerivce;
    
    private MockMvc mockMvc;
    
    @BeforeEach
    public void init(){
        mockMvc = MockMvcBuilders.standaloneSetup(userController).build();
    }
}
```

- @ExtendsWith(MockitoExtension.class) : Junit5와 결합하기 위한 어노테이션
- userService 가짜 객체를 생성하여 userController에 주입
- mockMvc : 함수 실행을 위해 메소드가 아닌 API가 호출되므로, API의 요청을 받아 넘겨줄 수 있는 별도의 객체

+) Spring Boot의 경우에는 @WebMvcTest도 사용 가능

<br />

<br />

**[1. 회원가입 성공 테스트]**

```java
@DisplayName("회원 가입 성공")
@Test
void signUpSuccess() throws Exception {
    //given
    final SignUpDTO signUpDTO = signUpDTO();
    doReturn(false).when(userService).isEmailDuplicated(signUpDTO.getEmail());
    doReturn(new User("a", "b", UserRole.ROLE_USER)).when(userService)
        .signUp(any(SignUpDTO.class));
    
    //when
    final ResultActions resultActions = mockMvc.perform(
    //perform에 대한 요청정보
    MockMvcRequestBuilders.post("/user/signUp")
    .contentType(MediaType.APPLICATION_JSON)
    .content(new Gson().toJson(signUpDTO)));
    
    //then
    final MvcResult mvcResult = resultActions.andExpect(status().isOk()).andReturn();
    final String token = mvcResult.getResponse().getContentAsString();
    assertThat(token).isNotNull();
}

private SignUpDTO signUpDTO(){
    final SignUpDTO signUpDTO = new SignUpDTO();
    signUpDTO.setEmail("su@test.test");
    signUpDTO.setPw("su");
    return signUpDTO;
}
```

- userService의 signUp 함수의 매개변수로 어떠한 변수도 처리함을 뜻하는 'any()'가 사용됨

  - HTTP Body로 전달된 데이터는 Spring에서 MessageConverter에 의해 새로운 객체로 변환됨

  - 이는 Spring에서 변환하는 것이므로, 우리는 API로 전달되는 SignUpDTO를 조작 불가능

    👉 SignUpDTO 클래스의 어떠한 객체도 처리할 수 있도록 any() 사용해야 함

- when 단계에서 보내는 객체는 Json이어야 하므로 Gson 활용해 변환

<br />

<br />

**[2. 이메일 중복으로 회원가입 실패 테스트]**

```java
@DisplayName("이메일이 중복되어 회원 가입 실패")
@Test
void signUpFailByDuplicatedEmail() throws Exception{
    //given
    final SignupDTO signUpDTO = signUpDTO();
    doReturn(true).when(userSerivce).isEmailDuplicated(signUpDTo.getEmail());
    
    //when
    final ResultActions resultActions = mockMvc.perform(
    MockMvcRequestBuilders.post("/user/signUp")
    .contentType(MediaType.APPLICATION_JSON)
    .content(new Gson().toJson(signUpDTO)));
    
    //then
    resultActions.andExpect(status().isBadRequest());
}
```

- 이 경우에는 userService의 signUp 메서드가 호출되지 않으므로, given 단계에서 제거해 주어야 함 (테스트는 stub에 엄격하므로 불필요한 stub이 있으면 테스트가 실패함)

<br />

<br />

**[3. 사용자 목록 조회 테스트]**

```java
@DisplayName("사용자 목록 조회")
@Test
void getUserTest() throws Exception{
    //given
    doReturn(userList()).when(userService).findAll();
    
    //when
    final ResultActions resultActions = mockMvc.perform(
    MockMvcRequestBuilders.get("/user/list"));
    
    //then
    final MvcResult mvcResult = resultActions.andExpect(status().isOk()).andReturn();
    final UserListResponseDTO response = Gson()
      .fromJson(mvcResult.getResponse().getContentAsString(), UserListResponseDTO.class);
    assertThat(response.getUserList().size()).isEqualTo(5);
    
}

private List<User> userList() {
    final List<User> userList = new ArrayList<>();
    for(int i=0; i<5; i++){
        userList.add(new User("su@test.test", "su", UserRole.ROLE_USER));
    }
    return userList;
}
```

- then 단계에서 Http Status가 OK 인지 확인하고, 주어진 Json 데이터를 객체로 변환하여 확인해보아야 함.

<br />

<br />

<br />

<br />

## 참고자료

https://mangkyu.tistory.com/143

https://mangkyu.tistory.com/144

https://mangkyu.tistory.com/145



추가 학습 자료 : https://devuna.tistory.com/39
