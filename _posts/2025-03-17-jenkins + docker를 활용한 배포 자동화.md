# Jenkins로 CI (continues integration) 구축
<img src=../assets/images/대략적인배포흐름.png width=50% height=50%>
대략적인배포흐름

```
Jenkins Server에 Docker 설치
Jenkins Server에 Docker를 이용하여 Jenkins 실행
Jenkins 접속
Jenkins Server 내부에서 Docker 사용할 수 있도록 Docker 설치
Jenkins와 Docker Hub 연결하기 위해 Credential 설정
Jenkins Server와 Spring Boot Server SSH 연결 하기 위해 Credential설정
Jenkins Pipeline 구성
Spring Boot Project Github Repository Clone
Gradle Build
Docker Image Build
Docker Push -> Docker hub
Spring Boot Server SSH 연결
SSH 원격 서버에서 Docker Pull
SSH 원격 서버에서 Docker Run
```
## 1. Jenkins Server에 Docker를 이용하여 Jenkins 실행
```
 - Jenkins Server 에 Docker 설치확인
    * mobaxterm으로 리눅스 서버에 접속후 systemctl status docker  : ok!
 -  
```  
