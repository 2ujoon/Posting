---
description: SSH Server 컨테이너 설정 및 Jenkins 환경설정
---

# SSH + Docker 가 설치되어 있는 VM(컨테이너) 사용하기

## 개요

### 준비사항

* SSH Server 설치

```bash
# ssh server 설치
docker pull edowon0623/docker
# m1 mac 의 경우
# docker pull edowon0623/docker-server:m1

docker run --privileged -itd \
        --name docker-server \
        -p 10022:22 -p 8081:8080 \
        -e container=docker \
        -v /sys/fs/cgroup:/sys/fs/cgroup \
        edowon0623/docker:latest \
        /usr/sbin/init
        
<< 'COMMENT'
# 또는
docker run -itd \
        --name docker-server \
        -p 10022:22 -e container=docker \
        --tmpfs /run \
        --tmpfs /tmp \
        -v /sys/fs/cgroup:/sys/fs/cgroup:ro \
        -v /var/run/docker.sock:/var/run/docker.sock \
        edowon0623/docker:latest \
        /usr/sbin/init
        
# Apple silicon
docker run --privileged -itd \
           --name docker-server \
           -p 10022:22 -p 8081:8080 \
           -e container=docker \
           -v /sys/fs/cgroup:/sys/fs/cgroup:rw \
           --cgroupns=host \
           edowon0623/docker-server:m1 \
           /usr/sbin/init
COMMENT

# ssh server 동작 확인 (root / P@ssw0rd)
ssh root@localhost -p 10022
```



* 컨테이너 1 - Jenkins
* 컨테이너 2 - SSH Server, docker 가 설치되어 있는 상태(docker in docker)



## 플러그인 설치

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Publish Over SSH 설치



## SSH Server  설정

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Dashboard - Jenkins 관리 - System - Publish over SSH - SSH Servers
* Name : SSH Server 설정의 이름
* Hostname : Jenkins 는 컨테이너에서 구동되고 있으므로,  docker-server 컨테이너에 접근하기 위해 Hostname 에 localhost 가 아닌 도커 호스트의 IP를 설정한다.
  * **WSL 등의 환경에서는 호스트 IP 가 다를 수 있다.** ifconfig 로 확인할 것
* Username : root
* Remote Directory : 현재 디렉토리(.)로 지정한다. /root 가 설정된다.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Passphrase / Password : root 계정의 비밀번호
* Port : docker-server 컨테이너의 22 포트를 포워딩 하는 호스트의  10022번 포트로 설정

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Test Configuration 버튼을 눌러 테스트 결과 확인



##
