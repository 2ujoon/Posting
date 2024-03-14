# Jenkins 설치 및 설정

## Docker Hub 에서 이미지 pull

* [도커가 설치](../appendix/docker-ubuntu-22.04.md)되어 있어야 한다.
* 최신 jenkins 이미지 다운로드

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

* 정상 실행 시 컨테이너 ID hash 만 콘솔에 출력된다.

<pre class="language-bash"><code class="lang-bash">docker run -d \
    -v jenkins_home:/var/jenkins_home \
    -p 8080:8080 -p 50000:50000 \
    --restart=on-failure \
    --name jenkins-server \
<strong>    jenkins/jenkins:lts-jdk17
</strong></code></pre>

* docker ps 명령어로 정상적으로 컨테이너가 올라갔는지 확인한다.

```bash
CONTAINER ID   IMAGE                       COMMAND                  CREATED          STATUS          PORTS                                                                                      NAMES
59af39a96517   jenkins/jenkins:lts-jdk17   "/usr/bin/tini -- /u…"   3 minutes ago   Up 3 minutes   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp, 0.0.0.0:50000->50000/tcp, :::50000->50000/tcp   jenkins-server
```



## Jenkins 활성화

* Docker 컨테이너가 정상적으로 올라갔다면 `http://PUBLIC-IP:8080` 로 접속할 수 있다.

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

*   최초 접속 시 Administrator password 를 입력해 활성화 해야 한다.

    * 컨테이너 생성 시 -v 로 볼륨 옵션을 사용했다면 해당 위치의 파일을 확인한다.
    * 또는 컨테이너 실행 직후 로그를 확인한다. (`docker logs jenkins-server`)

    <figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>



## 초기 설정

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

* 별도의 admin 계정 생성한다.
* 이후 http://localhost:8080/ 으로 젠킨스에 접속한다.
