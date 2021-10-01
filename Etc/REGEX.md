<div align="center">
  <br />
  <h1>❔ 정규표현식이 무엇인가</h1>
  <br />
</div>

**특정 규칙을 가진 문자열의 집합을 표현**하는데 사용하는 형식 언어로 컴퓨터 과학의 정규 언어로부터 유래하였다.

# ✍ 정규표현식의 기본 원칙들

## 목차

1. [**📍 위치로 찾을때**](#1)
2. [**🔍 문자로 찾을때**](#2)
3. [**🔍 수량자**](#3)
4. [**📄 문자클래스**](#4)
5. [**정규표현식을 학습하기위한 사이트**](#5)
   <br />

<div id="1"></div>

## 📍 위치로 찾을때

| 메타문자 |                  설명                  | 기타 |
| :------: | :------------------------------------: | :--: |
| ^'문자'  | 문자열에서 '문자'로 시작하는 것을 찾음 |      |
| '문자'$  |  문자열에서 '문자'로 끝나는 것을 찾음  |      |

- **^hi**

  - **hi**hellohi

- **hi$**

  - hihello**hi**

<br />

<div id="2"></div>

## 🔍 문자로 찾을때

|    메타문자    |                     설명                     |                 기타                  |
| :------------: | :------------------------------------------: | :-----------------------------------: |
| 문자 클래스 [] |            []사이의 문자들과 매치            |                                       |
|   -(하이폰)    |             두 문자 사이의 범위              |                                       |
|      [^]       |    []안에서 사용하면 not을 의미하게된다.     | [^0-9] == 숫자를 제외한 문자만 매치됨 |
|     .(Dot)     | 줄바꿈 문자인 '\n'을 제외한 모든 문자와 매치 |                                       |
|       \|       |              or과 같은 역할을함              |                                       |

**Test : himymeminehi**

- **\[ ]**

  - **[mi]** : 문자m 혹은 i와 매치됨 -> h**im**y**m**e**mi**neh**i**
  - **[my]**. : 문자 m혹은 y와 매치되는 것 + . -> hi**mymemi**nehi
  - **\[him][hie]** : h,i,m중 하나와 매치되는 것과 h,i,e중 하나와 매치되는 것이 이어진 문자 -> **hi**my**memi**ne**hi**

- **.(Dot)**

  - **.** : 모든 문자와 매치됨 -> **himymeminehi**

  - **.....** : 5개의 문자와 매치 -> **himymemine**hi

  - **\\..\\.** : .과.사이의 모든 문자를 가리킨다.

    - .h.imymeminehi -> **.h.**imymeminehi

**Test : ABCDabcefghijklm12345789**

- **-**

  - ABCDEFGHIJKLMNOPQRSTUVWXYZ

  - abcdefghijklmnopqrstuvwxyz

  - 0123456789

  - **[A-g]** : A부터 Z + a부터 g까지 의 문자 -> **ABCDabcefg**hijklm12345789

  - **[C-Ka-d2-6]** : AB**CDabc**efghijklm1**2345**789

- **[^]**

  - **[^cd]** : CD를 제외한 문자 -> **AB**CD**abcefghijklm12345789**
  - **[^a-z]** : 알파벳 소문자를 제외한 문자 -> **ABCD**abcefghijklm**12345789**

**Test : Monday Tuesday Friday**

- **|**

  - **(on|ues|rida)** : on이거나 ues이거나 rida 인것들을 선택 -> M**on**day T**ues**day F**rida**y

  - **(Mon|Tues|Fri)day** : Mon이거나 Tues 이거나 Fri이면서 뒤에 day까지 선택 -> **Monday** **Tuesday** **Friday**

  - **..(n|es|i)day** : n이거나 es거나 i인 문자들뒤에 day가 있고 그 문자 앞에있느 문자 두개 까지 선택 -> **Monday Tuesday Friday**

<br />

<div id="3"></div>

## 🔍 수량자

| 개념  |                  설명                   |                   기타                    |
| :---: | :-------------------------------------: | :---------------------------------------: |
|  \*   |              0번이상 일치               |                                           |
|   +   |              1번 이상 일치              |                                           |
|   ?   |            0번 혹은 1번 일치            | ?수량자에 추가하면 *게으른 수량자*로 만듬 |
|  {n}  |             정확히 n번 일치             |                                           |
| {n,}  |             적어도 n번 일치             |                                           |
| {m,n} | 반복 횟수 m부터 n까지(m또는 n 생략가능) |    {2,3} == 2부터 3까지 반복횟수 매치     |

_게으른 수량자 : 요소를 최대한 적게 찾는 것._

_탐욕적 수량자 : 요소를 최대한 많이 찾음_

**Test : himymmeminehi**

- **\***
  - **m\*e** : m or e가 0번이상 일치하는 것 -> himy**mme**min**e**hi
- **+**

  - **m+e** : 1번이상 일치하는 것 -> himy**mme**minehi

- **?**
  - **m?e** : m 혹은 e가 있거나 없거나 -> himym**me**min**e**hi

**Test : -@- -AAA-- -- "_" -- _**

- **.\***
  - 모든 텍스트 선택 -> **-@- -AAA-- -- "_" -- _**
- **-A\*-**
  - 앞뒤로 -가 있으면서 A가 0개 이상 있음 -> -@- **-AAA-**- **--** "_" **--** _
- **\\\*+**
  - \*문자가 1개이상 있는 것
- **-@+-**
  - -사이에 @가 1개이상 있는 것
- **[^ ]+**
  - 공백이 없는 것이 1개 이상인 것 -> 띄어쓰기를 제외한 모든 텍스트 부분을 선택

**Peter Piper picked a peck of pickled peppers**

- **.{5}**

  - 5글자가 선택됨 -> **Peter Piper picked a peck of pickled pep**pers

- **[pti]{1,3}**
  - p,t,i 중 문자가 1개에서 3개있는 경우 ->Pe**t**er P**ip**er **pi**cked a **p**eck of **pi**ckled **p**e**pp**ers
- **[a-z]{3,}**
  - 영어 소문자가 3개 이상 선택되는 경우 -> P**eter** P**iper** **picked** a **peck** of **pickled** **peppers**

<div id="4"></div>

## 📄 문자클래스

| 메타문자  |                 설명                  |          기타           |
| :-------: | :-----------------------------------: | :---------------------: |
|    \d     |              숫자와 매치              |                         |
|    \D     |         숫자가 아닌 것과 매치         |                         |
|    \s     |         whitespace문자와 매치         |                         |
|    \S     |    whitespace문자가 아닌 것과 매치    |                         |
|    \w     |           숫자+문자와 매치            | 공백은 여기에 포함 안됨 |
|    \W     |      숫자+문자가 아닌 것과 매치       | 공백은 여기에 포함 안됨 |
| \b , .\ b |         word boundary 앞, 뒤          |                         |
| \B , .\B  | word boundary 앞 or 뒤 를 제외한 문자 |                         |

- 공백은 w에 포함되지 않는다.

<div id="5"></div>

## 정규표현식을 학습하기위한 사이트

- [정규표현식 개념](http://zvon.org/comp/r/tut-Regexp.html#Pages~Contents)
- [정규표현식 설명\_Microsoft Docs](https://docs.microsoft.com/ko-kr/dotnet/standard/base-types/regular-expressions)

- [정규표현식 사용\_퀴즈를 맞춰가며 학습할 수 있음](https://regexone.com/)

- [정규표현식을 테스트해볼 수 있는 사이트](https://regexr.com/)
