<div align="center">
  <br />
  <h1>git branch 전략</h1>
  <br />
</div>

##  목차

1. [**브렌치 전략을 왜 써야 할까?**](#1)
2. [**Branch Strategy 종류**](#2)
3. [**작업 과정 정리**](#3)


<br />

<br />

<div id="1"></div>

### **✅ 브렌치 전략을 왜 써야 할까?**
​
우리는 어느 브렌치가 최신인지 모른다.

프젝 잘 만들어놓고 배포까지 하고 싶은데 어떤 브렌치를 기준으로 merge 해서 배포할지 문제가 있다.
<br />

<br />
1.  branch 만들기 전에 develop branch 최신화 하기!
    -   develop 브랜치에서
    -   git fetch origin develop
    -   git pull origin develop
2.  본인이 작업할 branch 만들기 -> git checkout -b \[branch 이름\]
    -   branch 이름은 \[feat, refactor, fix 등등 git commit 메시지 컨벤션 참조\]/luxury-shop-\[이슈 번호\]로 하기로 했음.
    -   ex) feat/luxury-shop-1, refactor/luxury-shop-8
3.  작업하고 커밋하고 푸시하기 PR 보내기
4.  코드 리뷰를 받기
5.  코드리뷰 반영 후 merge 하기 직전 develop에서 충돌을 방지해야 함. -> 작업 전에 1번에서 최신화한 develop branch가 달라졌을 수도 있기 때문!
    -   git fetch
    -   git pull --rebase origin develop
    -   충돌 나면 해결하기. intelij 상단 메뉴 중 VCS -> Git Resolve Conflict 이용하면 편함
    -   git rebase --continue 등등 명령어 사용. 충돌 났을 때 모르겠으면 물어보기.
    -   git push -f origin \[자신이 만든 브랜치\]
    -   PR에서 Merge 버튼 누르기 or 직접 merge 하기

    -   본인이 올린 PR은 본인이 충돌 해결하고 merge 하기!


<div id="2"> </div>

### **✅ Branch-Strategy**
​
1\. **git flow** : 5가지의 브렌치를 이용해 운영하는 브렌치 전략
​
[https://techblog.woowahan.com/2553/](https://techblog.woowahan.com/2553/) <- 요거 참고하기 
​
-   주기적으로 배포를 하는 서비스에 적합하다.
-   가장 유명한 전략인 만큼 많은 IDE가 지원한다.
​
2\. **github-flow** : master 브렌치와 pull Reqeust를 활용한 단순한 브렌치 전략 <- 난 이걸 사용함
​
[https://github.com/jhj960918](https://github.com/jhj960918) <- 직접한 github-flow
​
-   브렌치 전략이 단순하여 git을 처음 접하는 사람에게도 유용하다 (이거 쓰세요....)
-   CI(지속적 통합)/CD(지속적 배포)가 자연스럽게 이루어진다. 
​
-   기능 개발 branch 생성하기 이름은 팀 rule 정하기 #feat-이슈 번호!!! 체계적인 분류가 없기 때문에 브렌치 이름은 의도를 아주 잘 드러내야 함
​


<br />


<br />

<div id="3"></div>

### **✅ 작업 과정 정리**

**Spring Boot 왜 사용할까요?**

1.  branch 만들기 전에 develop branch 최신화 하기!
    -   develop 브랜치에서
    -   git fetch origin develop
    -   git pull origin develop
2.  본인이 작업할 branch 만들기 -> git checkout -b \[branch 이름\]
    -   branch 이름은 \[feat, refactor, fix 등등 git commit 메시지 컨벤션 참조\]/luxury-shop-\[이슈 번호\]로 하기로 했음.
    -   ex) feat/luxury-shop-1, refactor/luxury-shop-8
3.  작업하고 커밋하고 푸시하기 PR 보내기
4.  코드 리뷰를 받기
5.  코드리뷰 반영 후 merge 하기 직전 develop에서 충돌을 방지해야 함. -> 작업 전에 1번에서 최신화한 develop branch가 달라졌을 수도 있기 때문!
    -   git fetch
    -   git pull --rebase origin develop
        -   충돌 나면 해결하기. intelij 상단 메뉴 중 VCS -> Git Resolve Conflict 이용하면 편함
        -   git rebase --continue 등등 명령어 사용. 충돌 났을 때 모르겠으면 물어보기.
    -   git push -f origin \[자신이 만든 브랜치\]
    -   PR에서 Merge 버튼 누르기 or 직접 merge 하기

-   본인이 올린 PR은 본인이 충돌 해결하고 merge 하기!
