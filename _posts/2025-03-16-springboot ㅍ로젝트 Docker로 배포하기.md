
# Springboot 프로젝트 Docker 로 배포하기

```
https://railly-linker.tistory.com/entry/Springboot-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-Docker-%EB%A1%9C-%EB%B0%B0%ED%8F%AC%ED%95%98%EA%B8%B0 참고
```

## 스프링부트 프로젝트 확인
```
....\2025\ktcloud-study\test-proj\backend-test01 폴더에 intellij 로 테스트용 스프링부트 프로젝트 만듦
build/libs/backend-test01-1.0-SNAPSHOT.jar 파일 생성 확인 : 포트 8081로 실행되게 설정함 (application.yml)

서버에 파일 복사
dshan/ci_cd_test/springboot_jar 폴더에 복사
  - Power Shell 에서
    * scp [파일명] [서버계정ID]@[서버계정IP]:[디렉토리위치]/[받을경로]
    * scp backend-test01-1.0-SNAPSHOT.jar dshan@192.168.7.97:/home/dshan/ci_cd_test/springboot_jar


```



## Docker 파일 만들기

### type 1
dshan/ci_cd_test/springboot_jar 폴더에 Dockerfile 을 작성한다

```
# 베이스 이미지
FROM openjdk:17-jdk-slim

# WORK DIR 지정
WORKDIR /apps

# 이미지 빌드 시 --build-args 로 넘길 인자
#ARG JAR_FILE=build/libs/*.jar

# 이미지 혹은 파일을 도커 이미지의 파일 시스템으로 복사
#COPY ${JAR_FILE} app.jar
COPY backend-test01-1.0-SNAPSHOT.jar /app/

# 노출 포트
EXPOSE 8081

# 이미지를 기반으로 컨테이너를 띄울 때 항상 실행되어야 하는 명령어
ENTRYPOINT ["java", "-jar", "app.jar"]

```
cd dshan/ci_cd_test/springboot_jar
docker build -t backend-test01:1.0 -f Dockerfile .
docker images 로 생성된거 확인
docker run --name backend-test -d -p 5000:8081 backend-test01:1.0
  - 바로 Exited 되서 docker logs backend-test 해보니
      Error: Unable to access jarfile app.jar
  -   

docker run --name backend-test -i -t -d -p 5000:8081 backend-test01:1.0
docker exec -it backend-test /bin/bash
로 들어가서 파일 확인해보니 app.jar 가 없다


docker rm backend-test




### type 2
```
# 베이스 이미지 설정
FROM ubuntu:22.04

# 기본 패키지 설치
RUN apt-get -y update
RUN apt-get -y upgrade

# 시간대 설정 (Asia/Seoul 시간대로)
RUN DEBIAN_FRONTEND=noninteractive TZ=Asia/Seoul apt-get -y install tzdata
RUN ln -fs /usr/share/zoneinfo/Asia/Seoul /etc/localtime && dpkg-reconfigure -f noninteractive tzdata

# OpenJDK 설치 !!!필요한 JDK 버전에 맞는 설치!!!
RUN apt install -y openjdk-17-jdk

# 프로젝트 jar 파일 복사
# !!!jar 파일 이름 수정!!!
COPY ../../../build/libs/backend-test01-1.0-SNAPSHOT.jar /app/

# 작업 디렉토리 생성 및 이동
WORKDIR /app

# Spring Boot 애플리케이션 실행
# !!!jar 파일 이름 수정!!!
CMD ["java", "-jar", "-Dspring.profiles.active=dev8080", "/app/backend-test01-1.0-SNAPSHOT.jar"]
```
## Docker 파일이 준비되었다면 해당 파일로 도커 이미지를 만듭니다.
```
docker image build --pull=true -f "./external_files/docker/server_docker/Dockerfile-Server-Dev" -t raillylinker/server_dev:latest .
```
-f 옵션으로 앞서 생성한 도커 파일의 경로를 입력하면 되고, -t 로 생성할 도커 이미지의 이름을 설정하면 됩니다.
