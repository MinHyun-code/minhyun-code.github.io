---
layout: post
title: "Proxy Tool (Burp Suit)"
subtitle: "취약점 점검"
category: "etc"
date: 2023-11-03
background: '/img/posts/Burp Suit main.png'
---

<br>

> Web Proxy Tool
>
> 프록시를 사용하여 네트워크에서 통신하는 HTTP request를 가로채 분석 및 수정할 수 있으며,
> 그 외에도 취약점 테스트를 하거나 해킹 공격을 수행할 수 있는 점검 도구이다.
>
> ex. Burp Suit, OWASP-ZAP, Acunetix

<br>

**Burp Suit Download: <https://portswigger.net/burp/communitydownload>**

`Professional은 유로`

<br>
<br>

**Temporary project, User Burp defaults 선택하여 진행**

![proxyTool](/img/posts/ProxyTool1.png)
 
<br>

![proxyTool](/img/posts/ProxyTool2.png)

<br>
<br>

**그러면 아래와 같은 화면 출력**

![proxyTool](/img/posts/ProxyTool3.png)


<br>
<br>

**Proxy 탭 > Options 탭 > 127.0.0.1 주소 설정 확인**

![proxyTool](/img/posts/ProxyTool4.png)

<br>
<br>

**인터넷 옵션 > 연결 탭 > LAN 설정**

![proxyTool](/img/posts/ProxyTool5.png)

![proxyTool](/img/posts/ProxyTool6.png)

<br>
<br>

**설정이 끝나면, Burp Suite 화면에서 Proxy 탭 > Intercept 탭 > intercept in on 설정**

Burp 화면에서 네이버 접속하면 아래와 같은 화면 출력

![proxyTool](/img/posts/ProxyTool7.png)

<br>
<br>
<br> 

**참고 URL : <https://hailey0.tistory.com/39>**
