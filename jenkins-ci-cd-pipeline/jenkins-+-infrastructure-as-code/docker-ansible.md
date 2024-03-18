---
description: Ansible Server 기동
---

# Docker 컨테이너로 Ansible 실행하기

## Ansible-server 이미지 다운로드

```bash
# Windows
docker pull edowon0623/ansible

# Apple silicon
docker pull edowon0623/ansible-server:m1
```



## 컨테이너 실행

```bash
# Windows
docker run --privileged \ 
           --name ansible-server -itd \
           -p 20022:22 -p 8081:8080 \
           -e container=docker \
           -v /sys/fs/cgroup:/sys/fs/cgroup \
           edowon0623/ansible /usr/sbin/init
           
vi /etc/sysconfig/docker # --selinux-enabled=false 로 수정
sed -i -e 's/overlay2/vfs/g' /etc/sysconfig/docker-storage
systemctl start docker

# Apple silicon
 docker run --privileged \ 
            --name ansible-server -itd \
            -p 20022:22 -p 8081:8080 \
            -e container=docker \
            -v /sys/fs/cgroup:/sys/fs/cgroup --cgroupns=host \
            edowon0623/ansible-server:m1 /usr/sbin/init
```



## 컨테이너 동작 확인

* 버전 확인 : `ansible --version`
* 클라이언트 정보 확인 : `vi etc/ansible/hosts`
  * [`docker network inspect`](../appendix/docker.md#docker-network-inspect) `bridge` : 도커 컨테이너들의 네트워크 정보 확인
  * 컨테이너의 IP 주소를 그룹에 등록할 수 있다.



## SSH Key 생성

* 매 번 각 서버에서 커맨드 실행 시 비밀번호를 입력할 수 없으므로, SSH key 를 사용하여 자동으로 처리할 수 있다.
* ansible-server 의 개인키와 공개키를 생성하고, 공개키를 배포한다.
* `ssh-keygen`
* `ssh-copy-id root@[클라이언트 IP]`
