---
layout: post
title: "lucy-xss-servlet-filter로 XSS 예방"
subtitle: "취약점 점검"
category: "java"
date: 2023-11-02
background: '/img/posts/codeImg.jpg'
---

`추후에 사용하게 되면 업데이트 예정`

<br>
<br>

> XSS (크로스 사이트 스크립팅)
>
>게시판이나 웹 메일 등에 JS와 같은 코드를 삽입해 개발자가 고려하지 않은 
><br>기능을 작동하게 하는 공격 (사용자 대상)

<br>
<br>

# lucy-xss-servlet-filter

네이버에서 개발한 XSS 방지를 위한 필터

<br>

### 장점

1. XML 설정 만으로 XSS 방어가 가능해짐
2. 비즈니스 레이어의 코드의 수정이 발생하지 않음
3. 개발자가 XSS 방어를 신경쓰지 않아도 됨
4. XSS 방어가 누락되지 않음
5. 설정파일 하나로 XSS 방어절차가 파악됨

<br>

- `pom.xml` dependency 추가

```xml
<dependency>
  <groupId>com.navercorp.lucy</groupId>
  <artifactId>lucy-xss-servlet</artifactId> 
  <version>2.0.1</version>
</dependency>
```

<br> 

- `web.xml` filter mapping 선언

```xml
<filter>
  <filter-name>xssEscapeServletFilter</filter-name>
  <filter-class>com.navercorp.lucy.security.xss.servletfilter.XssEscapeServletFilter</filter-class>
</filter>
<filter-mapping>
  <filter-name>xssEscapeServletFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
```

<br>

- rule 추가는 `/resources/lucy-xss-servlet-filter-rule.xml` 경로에 파일생성 후 작성

    아래는 기본 세팅이고 특수 정책이 있을 경우, defender를 사용하여 예외처리를 할 수 있다.

    global 필터링의 경우, 예외처리할 파라미터가 없을 시 생략한다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<config xmlns="http://www.navercorp.com/lucy-xss-servlet">
  <defenders>
    <!-- XssPreventer 등록 -->
    <defender>
      <name>xssPreventerDefender</name>
      <class>com.navercorp.lucy.security.xss.servletfilter.defender.XssPreventerDefender</class>
    </defender>

    <!-- XssSaxFilter 등록 -->
    <defender>
      <name>xssSaxFilterDefender</name>
      <class>com.navercorp.lucy.security.xss.servletfilter.defender.XssSaxFilterDefender</class>
      <init-param>
        <param-value>lucy-xss-sax.xml</param-value>  <!-- lucy-xss-filter의 sax용 설정파일 -->
        <param-value>false</param-value>      <!-- 필터링된 코멘트를 남길지 여부, 성능 효율상 false 추천 -->
      </init-param>
    </defender>

    <!-- XssFilter 등록 -->
    <defender>
      <name>xssFilterDefender</name>
      <class>com.navercorp.lucy.security.xss.servletfilter.defender.XssFilterDefender</class>
      <init-param>
        <param-value>lucy-xss.xml</param-value>  <!-- lucy-xss-filter의 dom용 설정파일 -->
        <param-value>false</param-value>    <!-- 필터링된 코멘트를 남길지 여부, 성능 효율상 false 추천 -->
      </init-param>
    </defender>
  </defenders>

  <!-- default defender 선언, 별다른 defender 선언이 없으면 default defender를 사용해 필터링 한다. -->
  <default>
    <defender>xssPreventerDefender</defender>
  </default>
  
  <!-- global 필터링 룰 선언 -->
  <global>
    <!-- 모든 url에서 들어오는 globalParameter 파라메터는 필터링 되지 않으며 
       또한 globalPrefixParameter로 시작하는 파라메터도 필터링 되지 않는다. -->
    <params>
      <param name="globalParameter" useDefender="false" />
      <param name="globalPrefixParameter" usePrefix="true" useDefender="false" />
    </params>
  </global>
  
</config>
```

<br> 

이렇게만 설정하면 request를 통해 전송되는 파라미터들에 공통적으로 필터가 먹히게 된다.

서블릿 필터 라이브러리에는 기본 XSS 필터 클래스도 포함되어 있기 때문에 

추가로 문자열 치환이 필요한 경우, 라이브러리에서 제공하는 함수를 이용할 수 있다. 

<br>
<br>

## ⭐⭐⭐ 주의 ⭐⭐⭐

서블릿 설정으로 적용하였기 때문에 form-data에 대해서만 적용된다.

JSP 태그 또는 el 태그로 변수를 출력하는 경우
```jsp
<p>이름 : ${username}</p>
<p>연락처 : ${mobile}</p>
<p>주소 : <%=address %></p>
```
스크립트가 실행될 수 있다.

<br>

## ⭐⭐⭐ 해결방법 ⭐⭐⭐ 

`jstl 사용`

```jsp
<!-- 최 상단에 태그라이브러리 선언 -->
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>

<!-- HTML Body -->
<p>이름 : <c:out value="${username}"/></p>
<p>연락처 : <c:out value="${mobile}"/></p>
<p>주소 : <c:out value="${address}"/></p>
```

또는 

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn" %>
<p>연락처 : ${not empty mobile? fn:escapeXml(mobile) : '02-1234-1234'}</p>
```

사용하면 스크립트가 실행되지 않고 텍스트로 입력되는 것을 확인할 수 있다.


<br>
<br>
<br> 

**참고 URL : <https://hailey0.tistory.com/39>**
