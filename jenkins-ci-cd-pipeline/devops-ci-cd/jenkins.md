---
description: Jenkins 소개
cover: ../../.gitbook/assets/image (15).png
coverY: 0
---

# Jenkins 소개

## 특징

* CI / CD 를 위한 대표적인 오픈소스 툴



### 장점

* 다양한 플러그인 연동 가능
  * 빌드 : Maven, Gradle, And 등
  * VCS : Git, SVN 등
  * 개발언어 및 환경 : Java, Python, Node.js 등
  * 정적 테스트 : SonarQube 등
* 통합 환경 구성에 용이
* 무료



### 단점

* 이슈 트래킹 소프트웨어(Jira, Redmine 등)와 연계하기에는 불편한 편
* 내장 기능이 비교적 부족
* 대체재 : CircleCI, TeamCity, Bamboo, GitLab 등



## Jenkins 파이프라인

<div data-full-width="false">

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

</div>

* 단위 테스트, 통합 테스트를 통과해야 인수 테스트 단계로 넘어감
* UAT 환경에서 검수 완료 후 운영 환경으로 배포
* 위전반적인 과정을 자동으로 처리할 수 있게끔 구성
* Jenkins 의 기본 작업 단위는 **Item**
  * 각 단계를 Item으로 만들 수 있음
  * 여러 Item을 묶어서 Jenkins 의 파이프라인을 구성할 수 있음
  * 그 과정에서 JenkinsDSL 을 이용한 Jenkinsfile 을 작성해 정의 가능
