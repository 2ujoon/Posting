---
description: 빌드 후 도커 호스트에 설치된 톰캣 서버로 빌드 결과물을 배포
---

# CI / CD 작업을 위한 Tomcat 서버 연동

## 플러그인 설치

<figure><img src="../../.gitbook/assets/image (40) (1).png" alt=""><figcaption></figcaption></figure>

* Deploy to container 플러그인 설치



## Item 생성

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

* Maven 프로젝트 Item 생성

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

* 하단에 기존 Item 의 이름을 넣으면 해당 설정을 그대로 가져와서 수정해 사용할 수 있다.



### 1. General, 소스코드 관리, Build

* 이전 글과 동일 ([Maven 프로젝트 생성](maven.md#id-1.-general))



### 2. 빌드 후 조치

#### 복사할 패키지 파일 지정

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

* 드롭다운 메뉴에서 Deploy war/ear to a container 추가
* WAR / EAR files : 컨테이너로 복사할 대상(패키지 파일)의 경로를 지정한다.

#### 컨테이너 추가

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

* 톰캣 9.x 버전 선택(Tomcat 9.x Remote)
* 톰캣 설치 및 사용자 정보가 설정되어 있어야 함 ([참고](../appendix/tomcat.md))

#### deployer 계정 추가

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

#### 인증 정보 및 Tomcat URL 설정

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

* deployer 계정을 선택한다.
* 톰캣 URL 지정 시 localhost 로 설정하면 안된다.
  * 여기서  localhost 는 jenkins 가 돌고 있는 컨테이너를 가리키므로, 도커를 구동시키는 기기의 IP 를 설정해야 한다.



## 빌드 및 결과 확인

### 1. 빌드 후 Console Output 확인

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption><p>Console Output</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption><p>생성된 war</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption><p>톰캣 manager app 화면</p></figcaption></figure>

* 빌드에 성공했다면, 톰캣 경로의 webapps 아래에 패키지 결과물이 존재한다.
  * Jenkins 컨테이너 내의 workspace 에서 톰캣 서버로 복사된 것
* 톰캣 관리자 화면에서 실행 중인 상태를 확인할 수 있다.
  * [http://localhost:8088/hello-world/](http://localhost:8088/hello-world/)



##
