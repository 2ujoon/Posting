# Ansible Playbook 사용하기

## Playbook 이란?

* 매번 실행하는 module 과 달리 사용자가 원하는 내용을 미리 작성해 놓은 파일
* 다수의 서버에 반복 작업을 처리하는 경우에 주로 사용한다.
* &#x20;yml 형식으로 작성한다.



## 1. ansible host 추가

### yml

* first-playbook.yml

```
---
- name: Add an ansible hosts
  hosts: localhost
  tasks:
    - name: Add an ansible hosts
      blockinfile:
      path: /etc/ansible/hosts
      block: |
        [mygroup]
        172.17.0.5

```

* /etc/ansible/hosts 파일에 그룹 정보를 추가하는 내용의 task 를 작성한다.
  * hosts 에 localhost 를 명시해 처리할 대상을 지정한다.
  * `block : |` 와 같이 **파이프를 작성해야 아래에 코드 블럭을 작성**할 수 있다.

### 실행

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>실행 결과</p></figcaption></figure>

* `ansible-playbook first-playbook.yml`



### 결과

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

* playbook 에서 명시한 task 가 정상적으로 처리되었다.
* _**멱등성을 보장**_하므로, 같은 playbook 을 반복적으로 실행하여도 결과는 동일하다.



## 2. 파일 복사하기

### yml

* playbook-sample1.yml

```
- name: Ansible Copy Example Local to Remote
  hosts: devops
  tasks:
    - name: copying file with playbook
      copy:
        src: ~/sample.txt
        dest: /tmp
        owner: root
        mode: 0644
```

* ansible 서버의 \~/sample.txt 파일을 devops 그룹 모두의 /tmp 에 복사한다.
* 이 때, 파일의 소유자는 root, 권한은 644로 복사한다.

### 실행

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### 결과

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* sample.txt 가 정상적으로 복사되었다.



## 3. 다운로드

### yml

```bash
# linux
---
- name: Download Tomcat9 from tomcat.apache.org
  hosts: devops
  tasks:
   - name: Create a Directory /opt/tomcat9
     file:
       path: /opt/tomcat9
       state: directory
       mode: 0755
   - name: Download Tomcat using get_url
     get_url:
       url: https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.87/bin/apache-tomcat-9.0.87.tar.gz
       dest: /opt/tomcat9
       mode: 0755
       checksum: sha512:https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.87/bin/apache-tomcat-9.0.87.tar.gz.sha512
```

* [OS 별 스크립트 파일](https://github.com/joneconsulting/jenkins\_cicd\_script/tree/master/playbook\_script)

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption><p>버전 변경으로 인한 tar.gz 파일주소 변경</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption><p>버전 변경으로 인한 체크섬 주소 변경</p></figcaption></figure>

* tomcat 버전이 달라질 수 있으므로 실제 파일과 체크섬 주소를 확인할 것([아카이브](https://dlcdn.apache.org/tomcat/))

### 실행

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

### 결과

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

* docker-server(172.17.0.4) 에 tar.gz 파일이 정상적으로 복사되었다.

