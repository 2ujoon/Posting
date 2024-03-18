---
description: 빌드 - 복사 - 이미지 생성 - 컨테이너 실행
---

# (실습) Docker Container 에 배포하기 2

## Item Configure 수정

* 이전 실습 내용의 [war 파일 구동](docker-container-1.md#war) 부분을 Exec command 설정으로 대체한다.

### Exec command 추가

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

* 빌드 후 조치 - Send build artifacts over SSH - SSH Server - Transfer Set - Exec command
  * 커맨드 작성

```bash
docker build --tag=cicd-project -f Dockerfile .
docker run -d p 8080:8080 --name mytomcat cicd-project
```

### 결과 확인

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption><p>Console Output</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption><p>docker images / docker ps</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption><p>호스트 PC 의 8081 로 요청 시 정상 동작</p></figcaption></figure>

* 빌드, 이미지 생성, 컨테이너 실행까지 정상적으로 완료

## 문제점

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

* 빌드에 성공했지만, 똑같이 다시 한 번 빌드하면 실패한다.
  * 이전 빌드의 `docker run` 에 의해 컨테이너가 올라간 상태에서 같은 이름의 컨테이너를 다시 올리려고 시도했기 때문
  * _멱등하지 않다._ -> 컨테이너, 이미지 삭제 등의 추가적인 조치가 필요하다.



