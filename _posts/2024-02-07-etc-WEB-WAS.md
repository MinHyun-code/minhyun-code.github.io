---
layout: post
title: "WEB, WAS"
subtitle: "기초다지기"
category: "etc"
date: 2024-02-07
background: '/img/posts/web was.png'
---

# WEB, WAS 란?

<br>
<br>

## WEB (Web Server)

`작성된 html 페이지 등을 네트워크에 종속되지 않고, 웹 서비스를 할 수 있음`

- 웹 브라우저 클라이언트로부터 HTTP 요청을 받아들이고, HTML 문서와 같은 웹 페이지에서 흔히 찾아볼 수 있는 자료 콘텐츠에 따라 HTTP에 반응하는 컴퓨터 프로그램
- HW에서 WEB : 위와 같은 프로그램을 실행하는 Server 장치

`ex. Apache, Nginx, IIS`

<br>

## WAS (Web Application Server)

`웹 서버 + 웹 컨테이너`

- 웹 브라우저 클라이언트로부터 웹 서버가 요청을 받으면 애플리케이션에 대한 로직을 실행하여 웹 서버로 다시 반환해주는 소프트웨어이다.
- 웹 서버와 DBMS 사이에서 동작하는 미들웨어로써, 컨테이너 기반으로 동작한다.

`ex. Tomcat, JBoss, WebLogic, WebSphere, Jeus(tmax), Jetty(이클립스), Resin`

<br>

### 웹 컨테이너 동작방식

- JSP와 서블릿을 실행시킬 수 있는 소프트웨어를 웹 컨테이너 또는 서블릿 컨테이너라고 한다.
- 웹 서버에서 JSP를 요청하면 컨테이너가 JSP파일을 서블릿으로 변환하여 컴파일을 수행하고, 서블릿 수행결과를 웹 서버에게 전달하게 됨
- JSP 컨테이너가 탑재되어 있는 WAS는 JSP페이지를 컴파일 해 동적인 페이지를 생성하는 것이다.

<br>
<br>

>                          -------------------------- WAS -----------------------
>                                 웹 서버                          웹 컨테이너
> 
> 클라이언트 -> 요청 ->  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  컨테이너로 전송  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ->  &nbsp;&nbsp;&nbsp;   JSP, Servlet 구동 환경 제공
> 
> 클라이언트 <- 응답 <- 결과 값 받아 client로 전송 (정적) <- 동적 data 처리
> 

<br>
<br>
<br>
<br>

## Web Server 와 WAS의 구성


**WAS와 Web Server를 분리하지 않은 경우**
- 모든 컨텐츠를 한 곳에 집중시켜 웹서버와 WAS 역할을 동시에 수행
- 스위치를 통한 로드 밸런싱, 사용자가 적을 경우 효과적

<br>

**WAS와 Web Server를 분리한 경우**
- 웹서버와 WAS의 기능적 분류를 고려해 효과적인 분산을 유도
- 정적인 데이터는 웹서버에서 처리, 동적인 데이터는 WAS가 처리

<br>

**WAS 여러개와 Web Server를 분리한 경우**
- WAS단을 프리젠테이션 로직과 비즈니스 로직으로 구분하여 구성
- 특정 logic의 부하에 따라 적절한 대응을 할 수 있지만 설계단계 유지보수 단계가 복잡해질 수 있다.

<br>

> WAS와 Web Server를 분리한 이유
> 
> - 기능을 분리하여 서버의 부하 방지
> - 물리적으로 분리하여 보안강화
> - 여러대의 WAS를 연결 가능
> - 여러 웹 어플리케이션을 서비스 가능

<br> 
<br> 
<br>


<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://lee-automation-lab.tistory.com/entry/IT%EA%B8%B0%EC%B4%88%EC%A7%80%EC%8B%9D-WEBWAS-%EB%9E%80WEB-WAS-%EB%8F%99%EC%9E%91-%EB%B0%A9%EC%8B%9D>
<https://helloworld-88.tistory.com/71>
<div>
