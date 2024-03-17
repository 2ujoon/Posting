---
description: CI / CD 의 대략적인 개요
cover: ../../.gitbook/assets/image (12) (1).png
coverY: 0
---

# CI / CD Workflow

## 전반적인 흐름

1. 이용한 형상관리 - Git
2. 리포지토리에서 변경된 소스를 polling - Jenkins, TravisCI, CircleCI
3. 소스를 빌드 - Maven, Gradle
4. 서버의 인프라 구조를 코드로 관리 및 실행 - Ansible, Terraform
5. 구성된 서버 환경에 빌드된 프로젝트가 배포됨 - K8s, containerd, Docker, cri-o



## Jenkins 를 이용해 도커로 배포한다면

<figure><img src="../../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

1. 애플리케이션 소스 커밋
2. Jenkins 에서 코드를 지속적으로 빌드 및 패키징
3. 컨테이너 이미지 생성
   1. 이미지 저장소(컨테이너레지스트리)에 생성된 이미지 업로드
4. K8s 연동
   1. 이미지 저장소에서 가져온 이미지로 컨테이너인스턴스 생성
   2. 스케줄링, 스케일링 작업 수행

\* Jenkins 에서 필요한 명령어들을 처리할 수 있음



##

