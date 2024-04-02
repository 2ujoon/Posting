---
description: 빌드 결과물을 SSH 를 이용해 다른 서버로 복사하는 과정
---

# (실습) Docker Container 에 배포하기 1

## Item 생성

### 유형

* My-Third-Project 복사 (Maven project)

### &#x20;빌드 유발

* Poll SCM : 체크 x

### 빌드 후 조치

* Deploy war/ear to a container 항목 제거
* **Send build artifacts over SSH** 항목 추가

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

* Name : Publish over ssh 에서 설정한 SSH 서버의 이름
* Source files : SSH 서버로 보낼 파일
* Remove prefix : 위 패턴의 파일들에서 제거할 접두어
  * target 을 제거할 접두어로 지정하지 않으면 디렉토리가 함께 복사된다.
* Remote directory : 파일을 복사할 위치



## 빌드 및 결과 확인

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Console Output</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>docer-server container 내부</p></figcaption></figure>

* Remove prefix 에서 target 을 지정하지 않으면 디렉토리 전체가 복사된다.
  * 정상적으로 지정할 경우 Remote directory 에 hello-world.war 만 존재한다.



## war 파일 구동

### Dockerfile 확인

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* tomcat 9.0 이미지를 받아 베이스 이미지로 사용하겠다.
* ./hello-world.war 파일을 /usr/local/tomcat/webapps 에 복사하겠다.

### docker 이미지 생성

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption><p>docker build</p></figcaption></figure>

* [`docker build`](../appendix/docker.md#docker-build) `-t docker-server -f Dockerfile .`
  * docker build : 도커 이미지를 생성한다.
  * \-t docker-server : 생성될 이미지의 이름을 "docker-server:latest"로 한다.
  * \-f Dockerfile : Dockerfile 의 경로를 지정한다.
  * . : Dockerfile 을 찾기 시작할 디렉토리를 현재 디렉토리로 지정한다.

<figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption><p>docker images</p></figcaption></figure>

* [`docker images`](../appendix/docker.md#docker-images)
  * Dockerfile 에서 지정한 tomcat:9.0 과 생성된 docker-server 이미지를 확인할 수 있다.

### 생성된 docker-server  컨테이너 기동

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption><p>docker in docker 에서 정상적으로 올라간 tomcat</p></figcaption></figure>

* `docker run -p 8080:8080 --name mytomcat docker-server`

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption><p>호스트 PC 의 컨테이너 목록</p></figcaption></figure>

*   호스트 PC 에서 최종적으로 이 tomcat 까지 도달하기 위해서

    * (1) : 호스트 PC
    * (2) : 호스트 PC 의docker-server 컨테이너
    * (3) : 호스트 PC 의 docker-server 컨테이너의 docker-server 컨테이너

    라고 한다면,

1. (1)의 8081 포트로 접근 -> (2)의 8080 포트로 포워딩
2. (2)의 8080 포트로 접근 -> (3)의 8080  포트로포워딩
3. (3)의 8080 포트는 tomcat 의 LISTENING 포트

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

* 호스트 PC 에서 localhost:8081 로 요청 시 위의 순서에 따라 생성된 tomcat 으로 요청한다.
