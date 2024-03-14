# Docker 설치(Ubuntu 22.04)

## 설치 환경

* Raspberry PI 4
  * 4GB RAM, 128GB Storage
* Ubuntu 22.04



## 설치

* [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)
*   Windows, Mac 및 여러 Linux Distro 에서 Docker Desktop 설치를 지원한다.

    이 게시물은   Ubuntu 22.04 CLI 환경에서 설치하므로, Docker Engine 설치에 대해 설명한다.

### unofficial 또는 이전 버전 삭제 (필요 시)

```
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```



### Docker Desktop, Docker apt repository, 수동 또는 스크립트를 다운 받아 설치

* 이 경우에는 apt repository(apt-get) 를 이용하여 설치한다.
* Docker apt repository 설정

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```



### 최신 버전 설치

```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```



### 설치 확인

```bash
sudo docker run hello-world
```

* 최초 실행 시 hello-world 이미지가 없으므로 latest 이미지를 pull 한다.
* 정상적으로 설치되었다면 hello-world 이미지의 내용이 표시된다.

```bash
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
