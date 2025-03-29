---
layout: post
title: "String, Builder, Buffer"
subtitle: "문자열"
category: "java"
date: 2024-04-15
background: '/img/posts/builder buffer.png'
---

## String 사용

String은 `불변성`을 갖는다. 

즉, 변하지 않는 문자열을 자주 사용할 경우 String을 사용하는 것이 성능면에서 유리하다.

<br>
<br>

## StringBuilder 사용

동기화를 지원하지 않는 반면, 속도면에서 StringBuffer보다 성능이 좋다. `가변성`

즉, `단일 스레드 환경`과 문자열의 추가, 수정, 삭제 등이 빈번하게 발생하는 경우 StringBuilder를 사용하는 것이 성능면에서 유리하다.

<br>
<br>

## StringBuffer 사용

동기화를 지원하여 멀티 스레드 환경에서 안전하게 동작할 수 있다. `가변성`

즉, `멀티 스레드 환경`과 문자열의 추가, 수정, 삭제 등이 빈번하게 발생하는 경우 StringBuffer를 사용하는 것이 성능면에서 유리하다.

<br>
<br>
<br>
<br>

<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://velog.io/@heoseungyeon/StringBuilder%EC%99%80-StringBuffer%EB%8A%94-%EB%AC%B4%EC%8A%A8-%EC%B0%A8%EC%9D%B4%EA%B0%80-%EC%9E%88%EB%8A%94%EA%B0%80>
<div>
