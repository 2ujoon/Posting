# Maven 프로젝트 생성

## Item 생성

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* [Maven 플러그인 설치 전 Item 생성 화면](../devops-ci-cd/item-project/#item-1)



### 1. General

* 설명을 적절히 입력한다.



### 2. 소스 코드 관리

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Git - 리포지토리 주소, 빌드할 브랜치를 지정한다.
  * private 리포지토리의 경우 Credentials 에 계정 정보를 추가해야 한다.
* 샘플 예제 프로젝트 주소 : [https://github.com/joneconsulting/cicd-web-project](https://github.com/joneconsulting/cicd-web-project)



### 3. Build

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

* Root POM : Maven 프로젝트의 설정파일인 pom.xml 을 지정한다.
* Goals and options
  * clean : 기존 빌드 결과물을 지우겠다.
  * compile : 컴파일(빌드) 하겠다.
  *   package : pom.xml 의 설정에 따라서 패키지 파일을 만들겠다.

      <figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>



### 4. 저장 후 빌드

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

* Console Output 에서 빌드 결과 확인

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

* 작업공간(Workspace) 에서 target 폴더 내에 war 파일이 생성된 것을 확인
* 컨테이너 내부에서도 확인할 수 있음



\#
