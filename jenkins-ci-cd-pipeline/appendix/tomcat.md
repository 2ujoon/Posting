# Tomcat 설치

## 1. Tomcat 9.x 다운로드

* apache tomcat 에서 9 버전을 다운로드 한다.([https://tomcat.apache.org/download-90.cgi](https://tomcat.apache.org/download-90.cgi))



## 2. 사용할 포트 설정

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

* 톰캣 경로/conf/server.xml
* Jenkins 가 8080 포트를 사용 중이므로, 톰캣의 기본 포트를 다른 번호로 수정한다.(8088 등)



## 3. 접속 제한 해제

<figure><img src="../../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

* 톰캣 경로/webapps/manager/META-INF/context.xml
* 톰캣 경로/webapps/host-manager/META-INF/context.xml
* Valve 태그에서 127.0.0.1 만 접속할 수 있도록 제한하므로 주석 처리



## 4. 사용자 추가

<figure><img src="../../.gitbook/assets/image (2) (2).png" alt=""><figcaption></figcaption></figure>

* 톰캣 경로/conf/tomcat-users.xml
* 주석 처리 된 role, user 태그 형식과 동일하게 사용자 정보 추가

```xml
  <role rolename="manager-gui"/>
  <role rolename="manager-script"/>
  <role rolename="manager-jmx"/>
  <role rolename="manager-status"/>
  <user username="admin" password="admin>" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
  <user username="deployer" password="deployer" roles="manager-script"/>
  <user username="tomcat" password="tomcat" roles="manager-gui"/>
```



## 5. 확인

<figure><img src="../../.gitbook/assets/image (3) (2).png" alt=""><figcaption></figcaption></figure>

* 톰캣 매니저 화면에서 정상적으로 동작하는지 확인한다.([http://localhost:8088/manager/html](http://localhost:8088/manager/html))



##
