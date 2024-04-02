---
description: Ansible 컨테이너 기동
---

# Ansible 설정과 작동 과정

## Ansible 컨테이너 기동

### 이미지 다운로드

```bash
# apple silicon
docker pull edowon0623/ansible-server:m1

# intel
docker pull edowon0623/ansible
```



### 컨테이너 기동

```bash
# apple silicon
docker run --privileged \
    --name ansible-server -itd \
    -p 20022:22 -p 8081:8080 \
    -e container=docker \
    -v /sys/fs/cgroup:/sys/fs/cgroup --cgroupns=host \
    edowon0623/ansible-server:m1 /usr/sbin/init
    
# intel
docker run --privileged \
    -itd --name ansible-server \
    -p 20022:22 -p 8081:8080 \
    -e container=docker \
    -v /sys/fs/cgroup:/sys/fs/cgroup \
    edowon0623/ansible:latest /usr/sbin/init

# 도커 실행이 되지 않았다면
vi /etc/sysconfig/docker
sed -i -e 's/overlay2/vfs/g' /etc/sysconfig/docker-storage
systemctl start docker
systemctl status docker
```



### 각 컨테이너들의 할당된 ip 주소 확인

* [`docker network inspect`](../appendix/docker.md#docker-network-inspect) `bridge`
  * docker-server : 172.17.0.4
  * ansible-server : 172.17.0.3
  * jenkins-server : 172.17.0.2
* ssh 또는 `docker exec` 로 접근하여 `hostname -i` 로 확인 가능



### Ansible client group 관리

* `ansible --version` 으로 ansible 설치 확인
* /etc/ansible/hosts 파일에서 관리된다. 없다면 생성한다.
* 그룹 지정 예시

```
[devops]
172.17.0.3
172.17.0.4

[db]
172.17.0.5
```

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption><p>컨테이너 구조</p></figcaption></figure>

* ansible-server 에서 다른 컨테이너로의 작업을 자동화 한다.

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption><p>패스워드가 아닌 키를 이용하여 접근</p></figcaption></figure>

* Ansible 에서 각 컨테이너로 접근 시 매번 패스워드를 입력하기 보다, ansible-server 에서 생성한 키를  각 서버에 복사해 두고 사용한다.



## 다른 컨테이너로의 ssh 접근

### 일반적인 ssh 접근

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption><p>기본적으로는 패스워드를 요구한다.</p></figcaption></figure>

* 별다른 설정 없이는 클라이언트에 접근하기 위해 패스워드를 요구한다.



### 키 기반 인증

#### 키 생성

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption><p><code>ssh-keygen</code> 명령어로 키 생성</p></figcaption></figure>

#### 클라이언트에 공개키 복사

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption><p>더 이상 패스워드를 요구하지 않는다.</p></figcaption></figure>

* `ssh-copy-id` 명령어로 서버의 공개키를 클라이언트에 복사해 키 기반으로 인증한다.

