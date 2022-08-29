데이터베이스 쿼리에서 자주쓰이는 Like 문법 정리
문자열에서 % (와일드카드 라고 부름) 을 사용하여 원하는 문자가 포함된 자료를 검색할 때
사용한다. 단순 포함 검색외에도 여러 사용법이 있어서 정리해본다.

### **1. 기본 사용법**
> 'SC' 로 시작하는 이름 검색

![](https://images.velog.io/images/alstjdwo1601/post/7c112528-e68b-457a-b000-773596c45687/image.png)

% 와일드카드의 의미는 어떤 것이 와도 상관이 없다는 의미이다.
SC로 시작하고 뒤에는 무엇이 와도 상관없기 때문에 'SC%' 를 LIKE 조건으로 주면
SC로 시작하는 모든 정보를 조회할 수 있다.

> 'ER' 로 끝나는 이름 검색

![](https://images.velog.io/images/alstjdwo1601/post/5975cda7-75a0-4d69-9644-486c17e4dd08/image.png)

ER로 끝나고 앞에는 무엇이 와도 상관없기 때문에 '%ER' 을 LIKE 조건으로 주면 ER로 끝나는 모든 정보를 조회한다.

> 'AM' 을 포함하는 이름 검색

![](https://images.velog.io/images/alstjdwo1601/post/986377bb-b786-4f1a-902e-273c8dacb2c4/image.png)

AM이 포함되고 앞뒤로는 무엇이 와도 상관없기 때문에 '%AM%' 을 LIKE 조건으로 설정


### 2. 고급 사용법

> 대소문자 상관없이 검색

![](https://images.velog.io/images/alstjdwo1601/post/8205a572-6c2b-47a7-98f9-bdf2b290c7ca/image.png)

LIKE는 기본적으로 대소문자를 구분하여 검색하기 때문에, 대소문자 구분없이 검색하려면 **UPPER, LOWER 함수**를 이용하여 칼럼의 값을 치환 후 검색해야 한다.

> 'SALES' 로 시작하는 직군을 제외(반대로 검색)

![](https://images.velog.io/images/alstjdwo1601/post/eec7fc5c-52e4-40ca-a885-8af513a19391/image.png)

NOT LIKE 를 이용하면 해당 조건을 포함하지 않는 데이터 조회가 가능하다.

> 'LIKE' 여러개 사용하여 검색

![](https://images.velog.io/images/alstjdwo1601/post/5d49bffb-6558-4bcc-b7b1-3437aa84d06e/image.png)

LIKE 조건을 동시에 여러개 걸어야 하는 쿼리를 만들어야해서 검색하다가
다음과 같은 LIKE 여러개 동시에 조건을 걸어 검색하는 것을 찾게 되었다.

### 3. 언더바( _ ) 사용법

> 다섯 자리 이름만 검색

![](https://images.velog.io/images/alstjdwo1601/post/03b2e113-1daf-4765-81ee-cc0b42de08f3/image.png)

언더바를 사용하여 검색할 **문자열의 자릿수를 결정**할 수 있다.

> 다섯자리 이름 중 마지막 문자가 'S' 인 사람 검색

![](https://images.velog.io/images/alstjdwo1601/post/1e7474ee-cdbc-49b8-905d-47d27a776823/image.png)

위와 같이 이름의 앞 4자리는 임의의 문자가 존재(자릿수가 중요)하고, 마지막에는 S가 존재하는 이름만 뽑도록 응용할 수 있다.

> 세번째 자리가 'A' 인 이름 검색

![](https://images.velog.io/images/alstjdwo1601/post/fc2bff3c-32c0-4a34-8a14-e0e5b2b767a1/image.png)

앞의 2자리는 임의 문자, 세번째 자리는 A이며 뒤에는 무엇이 와도 상관없다.


