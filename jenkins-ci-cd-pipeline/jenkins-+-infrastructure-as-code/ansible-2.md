---
description: ansible 모듈(명령어) 사용 테스트
---

# Ansible 모듈 사용

* [사용할 수 있는 모듈 목록](https://docs.ansible.com/ansible/2.9/modules/list\_of\_all\_modules.html)
* `ansible [그룹명] -m [모듈명] -a [인자]`



## 연결 상태 확인하기

* `ansible all -m ping`

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>ping 성공</p></figcaption></figure>

* 모든 그룹에 ping 이라는 모듈을 실행한다.
* 두 클라이언트에서 성공했음을 알 수 있다.

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>docker-server 컨테이너 종료 후 시도 시</p></figcaption></figure>

* 실패할 경우 결과와 함께 오류 메시지를 출력한다.



## 메모리 상태 확인하기

* `ansible all -m shell -a "free -h"`

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

* 모든 그룹에 shell 이라는 모듈을실행하고, "free -h" 를 인자로 넘긴다.
* 각 클라이언트에서 `free -h` 명령어가 실행된 결과를 반환받아 표시한다.



## 파일 복사하기

* `echo "Hey there" >> test.txt` : 테스트용 파일 생성
* `ansible all -m copy -a "src=./test.txt dest=/tmp"`

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption><p>실행 결과</p></figcaption></figure>

* 모든 그룹에 copy 모듈을 실행하고, "src=./test.txt dest=/tmp" 를 인자로 넘긴다.
  * src : 옮길 파일
  * dest : 목적지 경로

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption><p>test.txt 생성 확인</p></figcaption></figure>

* 정상적으로 복사된 것을 확인할 수 있다.



## 프로그램 설치

* `ansible devops -m yum -a "name=httpd state=present"`

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>httpd 설치 성공 메시지</p></figcaption></figure>

* devops 그룹에 yum 이라는 모듈을 실행하고, "name=httpd state=present" 를 인자로 넘긴다.

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption><p>httpd 설치 결과</p></figcaption></figure>

* httpd 가 설치된을것 확인할 수 있다.
