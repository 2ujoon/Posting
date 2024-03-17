# PollSCM 설정을 통한 지속적인 파일 업데이트

## Build periocally 와 Poll SCM

* cron job 이용
* Item 구성의 빌드 유발(Build Triggers) 메뉴에서 설정
  * Build periodically : 변경사항이 없어도 주기적으로 빌드
  * **Poll SCM : 새 커밋이 있을 경우에만 빌드**



## Poll SCM

<figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

* **\* \* \* \* \*** : 매 분마다빌드하겠다.
  * 너무 빈번해서 Jenkins 가 경고 표시
* 실제 환경에서는 무조건적인 배포 보다는, 테스트 실행 결과 등에 따라 적절히 배포할 필요가 있다.



## 반영 결과(예시)

### 변경 전

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

### 변경 후

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

* 매 분 확인 후 빌드하도록 설정했으나, 새로운 커밋이 있을 때만 빌드가 시작된 것을 확인할 수 있다.



##
