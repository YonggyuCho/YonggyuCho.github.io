---
layout: post
title: "CI/CD"
subtitle: "CI/CD 공부."
date: 2023-06-03
background: ''
categories:
  - Git
tags:
  - Git
  - Github
  - CI/CD
  - GithubAction
  - DevOps
---

# CI/CD란

**CI (Continuous Integration, 지속 통합)**

**CD (Continuous Deployment, 지속 배포)**

CI와 CD를 합쳐 CI/CD로 많이 불립니다.

어플리케이션 개발 단계부터 배포까지 자동화를 통해
빠르고 효율적으로 사용자에게 배포하는 개발 프로세스입니다.

CI 단계에서는 Main Repository에
코드 변경 사항을 주기적으로 빈번하게 Merge해야 합니다.
주기적인 단위는 아주 작은 단위여야 합니다.
지속적인 Merge가 자동으로 Build되고 UnitTest까지 자동화됩니다.

실패했을 경우 Red, 성공했을 경우 Green으로 알려줍니다.

CI를 통해 개발 생산성이 향상되고
버그 수정이 용이하며
문제점을 빠르게 발견할 수 있습니다.
*코드의 품질이 향상됩니다.

CD는 릴리즈와 배포 단계입니다.

결국 CI/CD는
Build, Test, 릴리즈, 배포 단계들이 전부 자동화된 것입니다.

여러 도구가 존재하지만 그 중 하나인 GitHub Actions를 알아보겠습니다.

# GitHub Actions

GitHub Actions은 5가지 개념이 중요합니다: **Events, Workflows, Jobs, Actions, Runners.**

**Events**

```yml
on:
  push:
  ```
GitHub에서 발생하는 특정한 이벤트(사건)들을 지정합니다.
예) main 브랜치로 merge하는 과정, 커밋을 푸시하는 과정, 이슈를 누군가 여는 과정 등.

**Workflows**

특정한 이벤트가 발생했을 때 내가 어떤 일을 수행하고 싶은지를 지정하는 것이 Workflows입니다.
자동화하고자 하는 것을 Workflows 안에 지정할 수 있습니다.
Workflows 안에는 하나 또는 여러 개의 Job이 존재합니다.

**Jobs**

하나의 Job 단위로 특정 행동을 합니다.
예) 어떤 Job은 유닛 테스트를 하고 또 다른 Job은 E2E 테스트를 합니다.
여러 개의 Job들은 동시에 실행되지만, Job끼리의 순서도 지정할 수 있습니다.

각각의 Job 안에는 Step(순서)을 지정할 수 있습니다.
예) Step 1: Action Checkout, Step 2: npm test

**Actions**

Step을 명시하는 과정에서 Actions를 사용합니다.
GitHub에서 제공하는 여러 개의 유용한 Actions입니다.
예) Action Checkout, Action Setup Node

**Runners**

Job들을 실행하는 것을 Runners라고 합니다.





