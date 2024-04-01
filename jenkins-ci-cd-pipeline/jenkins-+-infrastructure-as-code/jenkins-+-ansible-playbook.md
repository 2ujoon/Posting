# 실습) Jenkins + Ansible Playbook 사용하기

## 빌드 결과물을 Ansible-server 로 복사

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption><p>SSH 서버로 추가해 둔 ansible-host 사용</p></figcaption></figure>

* 다른 설정은 My-Docker-Project 와 동일
* 빌드 후 조치 - Send build artifacts over SSH 에서 ansible-host 를 추가한다.

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption><p>ansible-server</p></figcaption></figure>

* 빌드 해 보면 ansible-server 에서 hello-world.war 가 정상적으로 복사됨을 확인할 수 있다.



## Playbook 으로 docker image 생성

### playbook 작성

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption><p>first-devops-playbook.yml</p></figcaption></figure>

* 모든 호스트의 /root 위치에 있는 Dockerfile 을 이용해 cicd-project-ansible 이라는 도커 이미지를 생성한다.

### playbook 실행

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

* `ansible-playbook -i hosts first-devops-playbook.yml`
* `docker images` 로 playbook 의 결과물인 cicd-project-ansible 이미지가 생성되었다.



## playbook 으로 docker container 생성

### playbook 작성

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption><p>first-devops-playbook.yml</p></figcaption></figure>

* first-devops-playbook.yml 에 container 를 실행하는 task 를 추가한다.

### playbook 실행

<figure><img src="../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

* playbook 실행 후 새로운 컨테이너가 실행됨을 확인할 수 있다.
  * Jenkins 로부터의 실행을 확인하기 위해 컨테이너와 이미지 모두 삭제한다.

### Jenkins 에서 playbook 실행

<figure><img src="../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

* Send build artifacts over SSH 설정의 Exec command 에 playbook 커맨드를 추가하고 빌드한다.

<figure><img src="../../.gitbook/assets/image (90).png" alt=""><figcaption><p>빌드 성공</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (91).png" alt=""><figcaption><p>컨테이너 동작 확인</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (92).png" alt=""><figcaption><p>브라우저에서 확인</p></figcaption></figure>

* ansible-server 에서 my\_cicd\_project 컨테이너가 8080 포트로 동작한다.
  * **ansible-server 컨테이너의 8080 포트는 도커 호스트의 8081 포트와 포트포워딩** 되었으므로, 도커 호스트의 8081 포트로 접근해 my\_cicd\_project 컨테이너로 접근할 수 있다.



## 소스 코드 변경 시 이미지 빌드

### Poll SCM 설정 추가

<figure><img src="../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

* 빌드 유발 - Poll SCM - Schedule 에 cron 패턴을 작성한다.

### playbook 에서 실행 중인 컨테이너 종료 task 추가

<figure><img src="../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

* playbook 실행 시 이미 컨테이너가 실행 중인 경우 Jenkins 빌드 결과가 UNSTABLE 로 나타난다.
  * playbook 에서 현재 컨테이너와 이미지를 삭제하는 task 를 추가한다.
* 정상적으로 빌드 성공 시, 이미지와 컨테이너가 새로 생성된다.



##
