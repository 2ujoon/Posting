---
description: Cloud Native Application 를 구성하는 각 요소에 대한 간략한 설명
cover: ../../.gitbook/assets/image (4) (1) (1) (1).png
coverY: 0
---

# Cloud Native Application 의 구성 요소

##

## Cloud Native 란?

* 클라우드 컴퓨팅 환경에서 애플리케이션을 구축, 배포 및 관리하는 소프트웨어 접근 방식 또는 방법론

### Cloud Native의 특징

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* CI / CD : 개발된 애플리케이션의 빌드, 테스트, 배포 과정의 자동화



## MSA

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

* 마이크로서비스 개발
* Inner Architecture : 비즈니스 로직을 가지고 개발된 서비스
* Outer Architecture / Capability : 서비스 작동 및 운영을 지원해주기 위한 시스템



## Container

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

* 마이크로서비스들이 컨테이너 가상화 기술을 통해 클라우드 환경에 배포됨
* 다수의 MSA 앱을 실제 서버로 기동하면 리소스 낭비 및 많은 비용이 발생할 수 있음
*   docker

    * 대표적인 컨테이너 가상화 기술
    * 기존 서버 가상화에 비해 적은 리소스 사용 (레이어 공유 등)
    * DockerDSL 로 작성한 Dockerfile 을 토대로 이미지 생성
    * 생성된 이미지를 다른 시스템이나 환경(테스트, 운영) 등으로 구분해서 사용할 수 있음



## DevOps

### Development + Operations

* 서비스 장애, 사용자의 요구사항을 반영하기 위한 개발 - 운영 조직 간의 상호 협력
*   개발과 운영을 서로 다른 조직에서 관리되며 문제점이 대두

    * 개발 : 변화, 변경 목적
    * 운영 : 안정성 지향



### 특징

* 코드로 인프라 관리(IaC)
* 애자일, 린 스타트업, CI/CD 등을 지향
* 서비스 전반적인 부분에서 유기적으로 연결하고 관리하기 위한 일련의 과정이자 문화



## CI / CD

<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

### Continuous Integration

* 코드 컴파일, 테스트, 패키징이 포함됨
* 주기적, 빈번한 배포를 위해 작은 단위로 여러 번 배포하기 위함
*   통합을 위한 빌드, 테스트, 머지 등의 작업을 자동화하는 것

    * 생산성 향상, 빠른 문제 발견, 용이한 수정. 코드 품질 향상을 목적으로 함



### Continuous Delivery / Continuous Deployment

* CI의 결과물을 여러 곳으로배포
* Continuous Delivery, 지속적 제공
  * 변경사항이 테스트를 거쳐 리포지토리에 업로드
  * 이후운영팀이 리포지토리에서 프로덕션 환경으로 배포할 수 있음
  * 개발팀과 운영팀 간의 가시성, 커뮤니케이션 문제 등을 해소하는 효과가 있음
  * 최소 노력으로 새 코드를 배포하는 것이 목표
*   Continuous Deployment, 지속적 배포

    * 변경 -> 리포지토리 -> 운영환경 배포 과정을 자동으로 처리하는 것
    * 자동화로 인한 프로세스 간소화



###
