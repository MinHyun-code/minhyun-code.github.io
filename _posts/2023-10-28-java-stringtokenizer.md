---
layout: post
title: "StringTokenizer"
subtitle: "코딩문제 필수 개념"
category: "java"
date: 2023-10-28
background: '/img/posts/StringTokenizer.png'
---

# StringTokenizer

문자열을 구분자를 이용하여 분리할 때 사용하는 클래스

`BufferedReader 클래스`의 메서드로 입력을 받아들인다면 라인 단위로 읽을 수 밖에 없다.

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

// 만약 입력값이 10 10 이라면 
String temp = br.readLine(); // temp 변수의 값 = "10 10" 
```

위 temp 변수의 데이터를 나누기 위해서 `StringTokenizer`를 사용할 수 있다.

<br>

```java
// 1. 띄어쓰기를 기준으로 문자열을 분리
StringTokenizer st = new StringTokenizer(문자열);

// 2. 구분자를 기준으로 문자열을 분리
StringTokenizer st = new StringTokenizer(문자열, 구분자);


// 구분자를 기준으로 문자열을 분리할 때 구분자도 토큰에 넣는지의 여부 (Default : false)
StringTokenizer st = new StringTokenizer(문자열, 구분자, true/false);

```

<br>
<br>

### StringTokenizer 메서드

|리턴값|메서드명|역할|
|:---:|:---:|:---|
|boolean|hasMoreTokens()|남아있는 토큰이 있으면 true를 리턴, 더이상 토큰이 없으면 false를 리턴|
|String|nextToken()|객체에서 다음 토큰을 리턴|
|String|nextToken(String delim)|delim 기준으로 다음 토큰을 리턴|
|boolean|hasMoreElements()|hasMoreTokens와 동일|
|Object|nextElement()|nextToken 메서드와 동일하지만 문자열이 아닌 객체를 리턴|
|int|countTokens()|총 토큰의 개수를 리턴|