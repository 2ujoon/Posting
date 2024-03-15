# Jenkins 설치 및 설정

## Docker Hub 에서 이미지 pull

* [도커가 설치](../appendix/docker-ubuntu-22.04.md)되어 있어야 한다.
* 최신 jenkins 이미지 다운로드
* [`docker pull`](../appendix/docker.md#docker-pull)

{% code fullWidth="false" %}
```bash
docker pull jenkins/jenkins
# 사용자 jenkins 의 jenkins 리포지토리를 pull 받겠다
```
{% endcode %}

* 또는  lts-jdk17 태그 이미지 다운로드

```bash
docker pull jenkins/jenknins:lts-jdk17
```



## 컨테이너 실행

* [`docker run`](../appendix/docker.md#docker-run)
* 정상 실행 시 컨테이너 ID hash 만 콘솔에 출력된다.

```bash
docker run -d \
    -v jenkins_home:/var/jenkins_home \
    -p 8080:8080 -p 50000:50000 \
    --restart=on-failure \
    --name jenkins-server \
    jenkins/jenkins:lts-jdk17
```

* docker ps 명령어로 정상적으로 컨테이너가 올라갔는지 확인한다.

```bash
CONTAINER ID   IMAGE                       COMMAND                  CREATED          STATUS          PORTS                                                                                      NAMES
59af39a96517   jenkins/jenkins:lts-jdk17   "/usr/bin/tini -- /u…"   3 minutes ago   Up 3 minutes   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp, 0.0.0.0:50000->50000/tcp, :::50000->50000/tcp   jenkins-server
```



## Jenkins 활성화

* Docker 컨테이너가 정상적으로 올라갔다면 `http://PUBLIC-IP:8080` 으로 접속할 수 있다.
* 컨테이너에 JDK가 존재해야 정상적으로 구동한다.

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

*   최초 접속 시 Administrator password 를 입력해 활성화 해야 한다.

    * 컨테이너 생성 시 -v 로 볼륨 옵션을 사용했다면 해당 위치의 파일을 확인한다.
    * 또는 컨테이너 실행 직후 로그를 확인한다. ([`docker logs`](../appendix/docker.md#docker-logs) `jenkins-server`)

    <figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>



## 초기 설정

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

* 별도의 admin 계정을 생성한다.
* 이후 젠킨스에 접속 시 사용할 URL을 설정한다.(http://localhost:8080/)



## 설정 확인

### JDK(JDK Installations)

* Jenkins 관리 -> Global Tool Configuration(또는 Tools)&#x20;
* JDK 를 따로 설치했거나, 빌드에 사용되는 JDK를 다른 버전을 사용하고 싶을 때 해당 JDK의 이름과 경로를 명시해야 한다.
* jenkins-server 컨테이너 내에서 설치된 JDK 경로를 찾을 수 있다.
  * `echo $JAVA_HOME` 또는 `env | grep JAVA` 등
* Install automatically 를 선택해 자동 설치할 수 있다.
  * Oracle 계정이 요구되며 최근 버전의 JDK 를 지원하지 않음



##
