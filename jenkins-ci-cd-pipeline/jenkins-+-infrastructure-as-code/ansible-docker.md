---
description: playbook 으로 docker hub 에 이미지 업로드
---

# Ansible 을 이용한 Docker 이미지 관리

## Docker hub 에 직접 이미지 업로드

### 이미지에 계정명 추가

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>docker tag</p></figcaption></figure>

* [`docker tag`](../appendix/docker.md#docker-tag) `이미지명[:태그명] 변경할이미지명[:태그명]` 으로 이미지에 계정명 추가
  * image id 는 동일하면서 이름만 다른 도커 이미지가 생성됨(wjleefusionsoft/cicd-project-ansible)

### docker registry 로그인

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>docker login</p></figcaption></figure>

* `docker login` 으로 레지스트리에 로그인 한다.
  * 이 때, 레지스트리를 명시하지 않으면 기본적으로 docker hub 에 로그인 된다.
  * 경고에서 볼 수 있듯, 비밀번호가 암호화 되지 않은 상태로 저장되므로 공용 PC 에서는 주의할 것

### docker hub 에 push

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption><p>docker push</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>docker hub </p></figcaption></figure>

* `docker push 이미지명` 으로 이미지를 업로드 한다.
* 레지스트리를 명시하지 않았으므로, 도커 허브에 이미지가 업로드 된다.



## Playbook 으로 도커 이미지 업로드

### playbook 작성

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>create-cicd-devops-image.yml</p></figcaption></figure>

* 도커 이미지를 생성하고 Docker hub 에 업로드 후 해당 이미지를 삭제한다.

### playbook 실행

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>docker hub</p></figcaption></figure>

* Docker hub 에 정상적으로 push 되었다.

## Playbook 으로 컨테이너 생성

* hosts 에 ansible-server(172.17.0.4), docker-server(172.17.0.3) 가 모두 등록되어 있는 상황으로 실습한다.

1. ansible-server 에서는 도커 이미지를 push 하는 작업만 수행
2. docker-server 에서는 해당 이미지를 pull 받아 컨테이너를 실행하는 작업만 수행

### Ansible-server 에서 docker image push

<figure><img src="../../.gitbook/assets/image (98).png" alt=""><figcaption><p><code>ansible-playbook -i hosts create-cicd-devops-image.yml --limit 172.17.0.3</code></p></figcaption></figure>

* `ansible-playbook -i hosts create-cicd-devops-image.yml`` `_**`--limit 172.17.0.3`**_
* `--limit` 옵션으로 특정 호스트에서만 실행되도록 지정할 수 있다.

### playbook 작성

<figure><img src="../../.gitbook/assets/image (97).png" alt=""><figcaption><p>create-cicd-devops-container.yml</p></figcaption></figure>

* 이미지명에 계졍명이 적혀있는지 확인할 것
* Dockerfile 로 이미지를 생성(`docker build`)하지 않고 Docker hub 에서 받아온다.

### playbook 실행

<figure><img src="../../.gitbook/assets/image (99).png" alt=""><figcaption><p>ansible-playbook -i hosts create-cicd-devops-container.yml --limit 172.17.0.3</p></figcaption></figure>

* `ansible-playbook -i hosts create-cicd-devops-container.yml`` `_**`--limit 172.17.0.4`**_
* 이 커맨드는 ansible-server 컨테이너에서 실행되었다.
  * 처음에는 docker-server 컨테이너에 이미지, 컨테이너 모두 없기 때문에 컨테이너 종료 / 삭제, 이미지 삭제 task 에서 에러가 발생했고, `ignore_errors: yes` 옵션에 의해 무시되었다.
  * playbook 을 한번 더 실행해 보면 오류 없이 완료된다.

<figure><img src="../../.gitbook/assets/image (100).png" alt=""><figcaption><p>docker-server 컨테이너에서 확인</p></figcaption></figure>

* **docker-server 컨테이너에서** docker hub 의 이미지를 이용해 컨테이너를 실행시켰다.



##
