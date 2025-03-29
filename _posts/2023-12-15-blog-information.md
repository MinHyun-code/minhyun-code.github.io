---
layout: post
title: "개발 정보 및 배포"
subtitle: "INFORMATION"
category: "blog"
date: 2023-12-15
background: '/img/posts/information.png'
---

> 언어 : Java, Html, CSS, MySQL
> 
> 기술 : Spring Boot, JPA, Spring Security, tiles, gradle
> 
> 배포 : AWS(EC2)
> 
> DB : AWS(RDS)
> 
> 개발환경 os : Windows
> 
> 배포환경 os : linux

<br> 
<br> 
<br>

## 리눅스 서버 접속 방법

1. EC2 인스턴스 생성할 때 만들었던 `프라이빗 키(pem)` 가지고 있어야함. 

2. 접속할 인스턴스 정보 클릭 > 연결 버튼 클릭

3. SSH 클라이언트 탭 클릭 > `ssh -i 명령어 복사`

4. cmd에서 프라이빗 키(pem) 위치로 이동 후 명령어 붙여넣기

5. 접속

<br>
<br>

## 반영 방법

1. 서버 접속 후 MINLOG 폴더로 이동

2. `jobs`, `jps`로 구동되는지 확인 - `kill PID`로 제거

3. `rm -r build` - 기존 build 파일 제거

4. `git pull origin main` - 최신 소스 가져오기

5. `./gradlew bootWar` - 빌드

6. /MINLOG/build/libs 폴더로 이동

7. `nohup java -jar 빌드된 War 명 &` - jar 파일 실행

<br> 
<br> 
<br>
