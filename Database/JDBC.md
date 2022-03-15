## JDBC란?


JDBC (Java Database Connectivity) 란 Java에서 데이터베이스와의 연결을 하고 SQL을 실행하기 위해 필요한 API이자 드라이버라고 생각하면 됩니다. Java 언어로 작성되고 플랫폼에 독립적이라는 특징을 가집니다.

![](https://images.velog.io/images/alstjdwo1601/post/9035900b-493b-4a56-8584-771276d5c53d/image.png)

- **JDBC API** : 데이터베이스 연동을 가능하게하는 JDBC 클래스는 자바 패키지 java.sql과 javax.sql에 포함되어 있다.
자바 애플리케이션에서 DB를 연결하고 데이터를 제어하기 위한 인터페이스와 클래스를 제공한다.

- **JDBC Driver Manager** : 애플리케이션이 요구하는 데이터베이스에 접근하기 위한 적절한 드라이버를 선택하여 데이터베이스와 연결하도록 해준다.

애플리케이션의 요청을 DBMS가 이해할 수 있는 프로토콜로 변환해주는 **클라이언트 사이드 어댑터이다.(서버가 아닌 클라이언트에 설치)**



----------------------------------

## JDBC 구조와 역할

JDBC는 크게 JDBC 인터페이스와 드라이버로 구성된다.
![](https://images.velog.io/images/alstjdwo1601/post/d543d19c-00ef-472b-b749-3f49c9f203a8/image.png)


애플리케이션에서는 SQL문을 만들어 JDBC 인터페이스에 전송하고 실제 구현 클래스인 JDBC 드라이버에서는 DBMS와 접속을 시도하고 SQL을 전송하는 구조를 가진다.

또한, DBMS에서 나온 결과를 역으로 거쳐 애플리케이션으로 가져오는 역할을 JDBC가 하기 때문에
애플리케이션과 DBMS의 다리 역할을 한다고 생각하면 된다.


----------------

## JDBC 의 사용법


Java 애플리케이션에서 JDBC를 구현하고 사용하기 위한 전제조건은 간단합니다. JDBC를 쓰려는 시스템에 Java 가 설치되어 있어야하며, 원하는 DBMS와 연결하기 위한 JDBC 드라이버 jar 파일이 필요합니다. 각각의 DBMS는 서로 다른 jar 파일을 가집니다.

저희가 알고있는 JPA는 개발자가 직접 쿼리를 짜거나 JDBC를 몰라도 객체지향적인 코딩에만 집중할 수 있게 도와주지만 내부적으로는 JDBC 를 사용합니다.  

JDBC를 Java 애플리케이션 내부에서 연결하고 사용하는 방식은 다음과 같습니다.

#### 1. import java.sql.*;
자바 애플리케이션에서 JDBC API가 구현되어있는 java.sql 패키지를 임포트합니다.

#### 2. 드라이버 로드 
ex) Class.forName("com.mysql.jdbc.Driver");
각각의 DBMS마다 이름은 다르지만 드라이버를 로드해줍니다.

#### 3. Connection 객체를 로드
![](https://images.velog.io/images/alstjdwo1601/post/2545be98-c55f-4a1d-9d2c-66e9ed92ca31/image.png)

DB와 연결을 하기위해 URL과 계정정보가 필요하기에 다음과 같이 가져옵니다.

#### 4. Statement 객체 생성
Statement stmt = con.createStatement();


#### 5. 쿼리 수행
![](https://images.velog.io/images/alstjdwo1601/post/bbf5f266-46c3-483d-a2ac-5aff8273321f/image.png)

#### 6. SQL 문에 결과물이 있다면 ResultSet 객체 생성
![](https://images.velog.io/images/alstjdwo1601/post/d538863f-d63f-464d-b211-7e5f1fb5155a/image.png)

next() 를 통해 테이블의 row 한 줄을 불러오거나
getString(), getInt() 를 통해 한 행의 특정 칼럼을 가져옵니다.


#### 7. 모든 객체 닫기
![](https://images.velog.io/images/alstjdwo1601/post/3b684f94-40c8-46a0-8414-9e750f6852c9/image.png)


----------

![](https://images.velog.io/images/alstjdwo1601/post/d92a7f01-70db-41ca-a058-5d7266b6f1cd/image.png)
