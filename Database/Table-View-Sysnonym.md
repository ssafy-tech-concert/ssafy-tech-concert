<div align="center">
  <br />
  <h1>Table-View-Synonym</h1>
  <br />
</div>

## 목차

1. [**Table-View-Synonym**](#1)
2. [**왜, 어떨때 사용하나?**](#2)
3. [**실제 사용**](#3)

<br />

<div id="1"></div>

## Table-View-Synonym

- <h3>1. Table</h3> 
  - 데이터들을 목록별로 정리해서 완성된 하나의 집합

- <h3>2. View</h3>
  - 사용자에게 접근이 허용된 자료만을 제한적으로 보여주기 위해 하나 이상의 기본테이블로부터 유도된 가상 테이블

- <h3>3. Synonym</h3>
  - ALIAS 같은 테이블의 이름을 변경한거나 줄일 때 사용. 보통 다른 유저의 객체를 참조할 때 많이 사용한다.

<img src="../images/synonym_1.png" alt="synonym_1" />

<br />


<div id="2"></div>

## 왜, 어떨때 사용하나?

View와 Synonym의 경우 보통 보안적인 문제로 인해 가장 많이 사용한다.
테이블에 필요한 데이터가 있지만 그것을 볼 수 있는 사용자와 볼 수 없는 사용자를 나누어야할 경우 View를 생성하여 보안이 필요한 데이터는 가리고, View에 대한 권한을 허용하는 방식.

Sysnonym의 경우는 더 은밀해진다. 이 테이블을 누가 만들어서 권한을 가지고 있는지도 감출 수 있다. 
다른 유저가 가지고 있는 객체를 참조할 경우 `[해당 유저의 이름.테이블의 이름]`의 형태로 호출 하기 때문에 어떤 유저에게 해당 테이블에 대한 권한을 가지고 있는지 노출되기 때문에 시노님을 만들어 해당 이름을 바꾸는 것이다.

<br />

<div id="3"></div>

## 실제 사용

테이블 생성

create table emp

select * from emp;

<img src="../images/synonym_2.png" alt="synonym_1" />

뷰 생성

create view emp_v
as Select empno, job, hiredate
from emp;

select * from emp_v;

<img src="../images/synonym_3.png" alt="synonym_1" />

시노님 생성

create synonym emp
for scott.emp_v;

<img src="../images/synonym_4.png" alt="synonym_1" />

select * from emp;

-> 시노님이 없다면?

select * from scott.emp_v;



같은 이름의 시노님, 테이블이 이 있을 경우 조회 우선순위는 정해져있다.

1. 테이블
2. private 시노님
3. public 시노님


<br>

