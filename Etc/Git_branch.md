<div align="center">
  <br />
  <h1>Git branch 전략</h1>
  <br />
</div>

## 목차

1. [**Git branch 전략이란**](#1)

<br />

<div id="1" />

## Git branch 전략이란?

Git branch 전략이란 여러 개발자가 1개의 저장소를 사용하는 환경에서 효과적으로 활용하기 위해 나온 개념입니다.

브랜치 생성, 병합 등을 사전에 설계한 전략에 맞게 Git 브랜치 구조를 만들어 보다 효율적으로 소스를 관리하고 협업을 원활하게 할 수 있도록 도와줍니다.

Git branch 전략에는 대표적으로 Git-Flow, GitHub-Flow, GitLab-Flow가 있습니다.

<br />

### 1. Git-Flow

가장 최초로 제안된 Workflow 방식입니다.

보통 대규모 프로젝트 관리에 적합한 방식으로 평가 받고 있습니다.

브랜치 종류는 총 5가지가 있습니다.

```
feature > develop > release > hotfix > master
```

master: 제품으로 출시되는 브랜치

develop: 다음 출시 버전을 개발하는 브랜치

feature: 기능을 개발하는 브랜치

release: 이번 출리 버전을 주입하는 브랜치

hotfix: 출시 버전에서 발생한 버그를 수정하는 브랜치

#### 장점

- 대규모 프로젝트 관리에 적합합니다.
- 에디터와 IDE 등에서 플러그인을 지원합니다.

#### 단점

- 브랜치가 많아 복잡합니다.
- 사용을 안 하거나, 애매한 포지션인 브랜치가 존재합니다.

<br />

### 2. GitHub-Flow

매우 단순한 흐름을 갖고 있는 브랜치 전략입니다.

[role] > master

master: 제품으로 출시되는 브랜치

[role]: 기능을 개발하는 브랜치

master 브랜치에 대한 role만 정확하다면 나머지 브랜치들에는 관여하지 않습니다.

#### 장점

- 브랜치 전략이 매우 단순합니다.
- 처음 Git을 접하는 사람에게 정말 좋은 시스템이 됩니다.

#### 단점

- 여러 작업들이 계속 올라오게되면 점점 꼬이게 됩니다.
- 버전을 관리해야 하는 시스템에는 치명적입니다.

<br />

### 3. GitLab-Flow

Github-Flow에서의 Flow가 너무나도 간단하여 배포, 환경 구성, 릴리즈에 대한 이슈가 있어 그것을 보완한 Flow입니다. 즉 Git-Flow는 너무 복잡하고 Github-Flow는 너무 단순하다 라는 요구사항에 나온 전략입니다.

```
master > pre-production > production
```

production: 제품으로 출시되는 브랜치(Git-Flow 에서의 master 브랜치와 같은 역할)

pre-production: master와 production 브랜치 사이에 pre-production 브랜치를 두어 변경 사항을 바로 production에 배포하지 않고 test server에 배포하여 통합 테스트를 진행하거나 시간을 두고 반영하는 브랜치입니다.(Git-Flow 에서의 release 브랜치와 같은 역할)

master: 다음 출시 버전을 개발하는 브랜치(Git-Flow에서의 develop 브랜치와 같은 역할)
