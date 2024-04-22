---
description: K8s 란?
---

# Kubernetes 소개

## 컨테이너 가상화의 역사

<figure><img src="../../.gitbook/assets/image (102).png" alt=""><figcaption><p>Back in time...</p></figcaption></figure>

### Traditional Deployment

* 하드웨어에 OS 설치 후 App 들을 올려 사용
* 특정 App 이 리소스를 많이 점유할 경우 다른 App 에 영향을 줄 수 있다.
* 서비스 확장이 어렵고 물리적인 서버를 유지하는 비용이 발생한다.



### Virtualized Deployment

* 서버 가상화
* VM 위에 개별적으로 OS 를 설치하여 운영한다.
  * 즉, 리소스를 독립적으로 운용하므로 App 들이 어느 정도 분리된 환경에서 동작한다.
* VM 이 늘어날수록 서버의 부담이 커지는 문제는 여전히 발생한다.



### Container Deployment

* 격리 수준이 약간 완화되었다.
* App 간 운영체제를 서로 공유한다.
  * 서버 가상화에 비해서 App 을 가볍게 운영한다.
* 서버의 인프라에 종속되지 않음으로써 클라우드에 대한 이식성이 높다.



## Kubernetes, K8s

### K8s 란?

* 컨테이너화 된 애플리케이션의 자동 배포, 스케일링 등을 제공하는 관리 플랫폼
* **Docker 를 대체하는 서비스가 아니다.** 상호 보완적이다.



### Do & Do not

| 컨테이너화 된 애플리케이션 구동     | 소스코드 배포, 빌드                     |
| --------------------- | ------------------------------- |
| 서비스 디스커버리, 로드 밸런싱     | application 레벨 서비스              |
| 스토리지 오케스트레이션          | 로깅, 모니터링                        |
| 롤아웃, 롤백 자동화           | 포괄적인 머신 설정, 유지보수, 관리, 자동 복구 시스템 |
| 빈 패킹 자동화(bin packing) |                                 |
| 복구 자동화(self-healing)  |                                 |
| 시크릿과 구성 관리            |                                 |



### K8s Cluster

<figure><img src="../../.gitbook/assets/image (103).png" alt=""><figcaption><p>K8s Cluster</p></figcaption></figure>

* K8s Cluster = Master Node + Worker Nodes
* master node 의 api 정보를 활용해 가용한 worker node 에 접근
  * K8s Proxy 에 의해 네트워크 규칙이 관리된다.

#### Master Node

* 각각의 노드들을 관리한다.
* 설정 정보, 사용자의 스케줄 관리, api 설계 등을 구성할 수 있다.

#### Worker Node

* 컨테이너를 운영하는 작업(스케일링 등)을 수행한다.
* 컨테이너를 관리하기 위한 pod, pod 를 운영하기 위한 kubelet 등으로 포함된다.



### 기본적인 구성

<figure><img src="../../.gitbook/assets/image (101).png" alt=""><figcaption><p>Working of K8s</p></figcaption></figure>

* Pod&#x20;
  * K8s 작업에서의 최소 단위
  * K8s 가 사용하는 리소스(또는 오브젝트)
  * 애플리케이션을 위해 상호 작용하는 컨테이너들의 논리적 집합
  * 여러 컨테이너들을 묶어 하나의 파드로 구성될 수 있다.
  * 노드는 컨테이너를 운영하기 위한 엔진을 가지고 있어야 한다.
* Service : 각 파드 간의 네트워크 작업(로드 밸런싱 등) 을 수행한다.
* 하나의 노드로도 구성할 수 있지만, 안정적인 서비스를 위해서는 여러 개의 노드로 클러스터를 구성하는 것이 일반적이다.

