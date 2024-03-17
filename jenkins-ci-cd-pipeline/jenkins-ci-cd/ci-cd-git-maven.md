# CI / CD 를 위한 Git, Maven 설정

## Github 플러그인 설정

### Git(Github) 플러그인 설치

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

* 설치된 플러그인에서 Github 확인 후 없다면 Available plugins 에서 설치



### Git 플러그인 설정

* Jenkins 관리 - Tools - Git Installation

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

* Path to Git executable 의 경우 가용한 git 커맨드를 의미한다. 별다른 설정이 없다면 git.
* jenkins-server 컨테이너 내에서 git 이 설치되었는지 확인할 것(`git version` 등)



## Maven 플러그인 설정

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

* Github 플러그인과 동일한 방법으로 Maven Integration 플러그인 설치 확인

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* 컨테이너에 Maven 이 설치되어 있는지 확인(`mvn --version`) 후 없다면 바로 설치할 수 있다.
