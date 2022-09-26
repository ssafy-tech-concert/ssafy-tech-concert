<div align="center">
  <br />
  <h1>Jenkins Pipeline</h1>
  <br />
</div>

## 목차

1. [**Jenkins Pipeline**](#1)
2. [**Pipeline의 이점**](#2)

<br />

<div id="1"></div>

## Jenkins Pipeline

Jenkins에서 지속적인 배포 파이프라인 구축을 지원하는 플러그인의 모음이다.

여기서, `지속적인 배포 파이프라인` 란, 소프트웨어에 대한 모든 변경이 배포되는 과정에서 거치는 복잡한 프로세스의 자동화된 표현을 말한다.

Jenkins Pipeline은 `DSL(Domain-Specific Language) Syntax`를 통해 다양한 파이프라인 모델링을 위한 도구를 제공한다.

## Jenkinsfile

Jenkinsfile을 통한 Pipeline 정의. `Piepeline-as-code` 의 기초로써, cd 파이프라인을 응용프로그램의 일부로 취급하여 다른 코드와 마찬가지로 버전 관리 및 검토를 한다.

### jenkinsfile의 이점

- 모든 branches 와 pull Request들로 파이프라인 빌드 프로세스를 자동적으로 생성할 수 있다.
- 파이프라인의 코드 리뷰 및 반복
- 파이프라인의 감사 추적(시간 순서에 따라 기록된 사용 내역)
- `Single Source of Truth(SSOT)` 즉, 프로젝트의 멤버들이 볼 수 있고, 수정이 가능하다는 이점이 있다.

<br />

<div id="2"></div>

## Pipeline의 이점

- Code
  - 코드로 구현되어 있기 때문에, 팀이 이 파이프라인을 편집 및 검토등 할 수 있음 (SSOT)
- Durable (내구성)
  - 프로젝트를 재시작했을때, Pipeline도 재시작함
- Pausable
  - 파이프라인을 선택적으로 중지하고, 다른 사람의 입력이나 승인을 기다릴 수 있음
- Versatile (다목적성)
  - 복잡한 실제 CD 요구 사항들을 지원함( fork/join,loop,perform)
- Extensible (확장성)
  - DSL에 의한 확장성과 다른 플러그인과의 통합을 위한 여러 옵션들을 지원함

### Freestyle 과 pipeline 의 차이점

이 세가지 과정을 수행해야 한다고 할때, Freestyle을 통해 만들었을때와 Pipeline을 사용하여 만들었다고 하자.

f1 : `echo hello1`

f2 : `sleep 60`

f3 : `echo hello2`

### Freestyle log

![image](https://user-images.githubusercontent.com/58917737/192285100-1c0b6e0d-8111-4743-ae76-9d81a9018e5b.png)

### Pipeline log

![image](https://user-images.githubusercontent.com/58917737/192285186-30fbc060-31bc-41fc-8ca3-2852f1768189.png)

Jenkins를 중간 kill 시키고, 다시 진행시켰을때,

Pipeline은 어느 지점에서 kill되었고, restart 시킨 부분까지 모두 보여진다.

![image](https://user-images.githubusercontent.com/58917737/192285270-74a879cf-2eb5-44ee-828d-78a8c1468ba2.png)

<br />

<div id="3"></div>

## Reference

- [CloudBeesTV - [What is Difference Between Freestyle and Pipeline in Jenkins]](https://www.youtube.com/watch?v=IOUm1lw7F58&t=336s)
- [Jenkins Pipeline Docs](https://www.jenkins.io/doc/book/pipeline/#why)
