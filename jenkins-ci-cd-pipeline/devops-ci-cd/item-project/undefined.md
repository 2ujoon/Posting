# 실습

## 1. Item 이름 및 유형 선택

* 이름 : My-First-Project
* 유형 : Freestyle project



## 2. Build Steps

* Execute shell
  * Execute shell 선택 후 적당한 echo 명령어 실행 (`echo "Hello Jenkins"`)



## 3. 대시보드에서 Item 확인

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

* Item 생성 확인 후 선택



## 4. 빌드

<figure><img src="../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

* 지금 빌드를 눌러 빌드 시작



## 5. 결과 확인

<figure><img src="../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

* 완료 후 드롭다운 메뉴에서 Console Output 선택
* 또는 <img src="../../../.gitbook/assets/image (32).png" alt="" data-size="line">를 클릭해 콘솔 화면으로 바로 이동

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

* 프로젝트가 빌드된 위치 확인 (workspacce)
* 추가한 shell 커맨드(echo)
* 추가한 커맨드의 출력
* 빌드 결과(SUCCESS)



## 6. 프로젝트 구성 수정

<figure><img src="../../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

* 대시보드에서 최근 빌드 결과를 확인할 수 있음
* 대시보드 - 프로젝트 선택 - 구성

<figure><img src="../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

* shell 커맨드 추가(`javac -version`)



## 7. 빌드 및 결과 확인

<figure><img src="../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

* 수정된 구성으로 다시 빌드

<figure><img src="../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

* 변경된 구성에 따라 정상적으로 콘솔이 출력됨을 확인(javac  버전)



## 8. 컨테이너 내의 workspace 확인

* [`docker exec`](../../appendix/docker.md#docker-exec) 로 컨테이너 내부에 접근

<figure><img src="../../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

* `docker exec -it 컨테이너ID bash`
  * 컨테이너 ID는 --name 옵션으로 지정한 컨테이너 명으로 대체 가능
  * \-it 옵션과  bash 셸을 실행시켜 컨테이너 내에서 계속 명령어 실행
* 빌드 결과 화면에서 확인한 workspace 경로로 이동
  * 빌드 과정에서 패키징을 하지 않으므로, 해당 경로에는 아무런 결과물이 없는 것이 정상



##
