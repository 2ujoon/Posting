---
description: Jenkins 에서의 Ansible 설정
---

# Jenkins + Ansible 연동하기

## SSH Server 추가

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

* 컨테이너(jenkins-server)에서 컨테이너(ansible-server) 로 연결하므로 내부 ip 를 사용한다.
* 같은 이유로 포트 번호 또한 20022번이 아닌 22번을 사용한다.
* 설정 완료 후 Test Configuration 확인할 것
