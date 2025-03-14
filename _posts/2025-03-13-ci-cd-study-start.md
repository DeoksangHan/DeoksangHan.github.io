---
layout: single
title:  "ci-cd-study-start!"
---

# git 관련 
[Git-Flow 브랜치 전략](https://velog.io/@mw310/Git-Flow-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EC%A0%84%EB%9E%B5).
```
브랜치 전략이란 여러 개발자가 하나의 저장소를 사용하는 환경에서 저장소를 효과적으로 활용하기 위한 work-flow다. 
브랜치의 생성, 삭제, 병합 등 git의 유연한 구조를 활용해서, 각 개발자들의 혼란을 최대한 줄이며 다양한 방식으로 소스를 관리하는 역할을 한다.
즉, 브랜치 생성에 규칙을 만들어서 협업을 유연하게 하는 방법론 설명
```


# 배포 관련  
[Nginx+Spring Boot 무중단 배포 구축하기](https://velog.io/@mw310/NginxSpring-Boot-%EB%AC%B4%EC%A4%91%EB%8B%A8-%EB%B0%B0%ED%8F%AC-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0)
```
nginx를 이용한 무중단 배포 방법 소개
```


# 스프링부트3 백엔드 개발자되기 도서 참고
   https://github.com/shinsunyoung/springboot-developer
   ```
   6장 소스 기반으로 테스트용 백엔드 샘플 만들어 두기
     - https://github.com/shinsunyoung/springboot-developer/blob/main/chapter6   의 소스 보면서 책과 함께..
     - intellij 로 실행 : 책 182page 까지만 구현 
   postman 으로 테스트
     - localhost:8080/api/articles 로 json post 하고 : 이때 local로 api 호출시 postman desktop agent 실행해두어야 한다 
     - localhost:8080/h2-console 로 확인
     - data.sql 만들어두고 : 189페이지 참조
        - 포스트맨 GET 테스트
           - localhost:8080/api/articles
     - 한글깨짐 관련
        Tabnine AI 설치 :deoksanghan / dshanid@naver.com / 비밀번호 자동생성 -> hdeoksang@gmail.com 에 저장 

 
   ```
## [Spring Boot] Gradle jar  빌드 및 배포하기
```
- IntelliJ 에서는 Gradle 탭에서 간단하게 생성이 가능합니다.
- 우측의 Gradle 탭에서 Tasks > build 안에 실행 가능한 bootJar 스크립트를 더블클릭하면 됩니다.
- build/libs 폴더가 생성되었고, 아래와 같이 jar 파일이 생성된 것을 확인하실 수 있습니다.
```

## 12장 참고 CI/CD 따라 해보기
```
1. Git 설치 확인
  - cmd 창에서
     - git --version  : git version 2.44.0.windows.1
  - Git 설정 확인
     - git config --list
  - 사용자 이름, 이메일 주소 설정
    git config --global user.email "hdeoksang@gmail.com"
    git config --global user.name "DeoksangHan"
2. SSH key 생성
   - ssh-keygen -t rsa -C "hdeoksang@gmail.com"
     C:\Users\진진VR/.ssh/id_rsa, id_rsa.pub 파일 생성됨
   -C:\Users\진진VR/.ssh/id_rsa.pub 파일  메모장으로 열어서 복사한후 
3. 깃허브 액션 사용하기
  3.1 깃허브 리포지터리 생성하고 코드 푸시
    - 깃허브 홈페이지 에서 새 리포지터리 만듦
      - https://github.com/DeoksangHan/springboot-developer
        - https://github.com/DeoksangHan/springboot-developer.git  
        - 리포지터리 주소 복사한후
   3.2 인텔리제이 터미널에서 현재 프로젝트 폴더인지 확인후
      - git init
      - git remote add origin https://github.com/DeoksangHan/springboot-developer.git
      - ... git push ..  단계까지 갔는데 에러남
        remote: Invalid username or password.
        fatal: Authentication failed for 'https://github.com/DeoksangHan/springboot-developer.git/'
      - git push -u origin main 하니깐... 로그인 어쩌고 창이 나오면서 됨,...

      - 파일 하나 수정후 해보니 잘 작동함
         - git add .
         - git commit -m "second try"
         - git push origin main  
4. 깃허브 액션 스크립트 작성하기, CI
   - 397페이지 보면서 따라함  ci.yml 작성
   - git add .
   - git commit -m "CI file append"
   - git push origin main  
   - 이후 깃허브 페이지 에서 Actios 메뉴 화면에서 워크플로 초록색으로 변하는것 확인

5. 깃허브 액션 스크립트 작성하기, CD
   - 책에서는 AWS 에 배포하는 과정이므로 일단 중지한다 

```

    
