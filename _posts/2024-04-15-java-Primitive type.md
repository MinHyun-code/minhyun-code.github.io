---
layout: post
title: "Primitive, Reference type"
subtitle: "기초다지기"
category: "java"
date: 2024-04-15
background: '/img/posts/reference.png'
---

## Primitive Type (원시 타입)

`int`, `long`, `double`, `float`, `boolean`, `byte`, `short`, `char`

반드시 사용하기 전에 선언되어야 하며, 자료형의 길이는 운영체제에 독립적이며 변하지 않는다.

스택 메모리에 저장된다.

<br>

## Reference Type (참조 타입)

원시 타입을 제외한 타입 (문자열, 배열, 열거, 클래스, 인터페이스)

즉, 참조 타입은 Java에서 최상위 클래스인 java.lang.Object 클래스를 상속하는 모든 클래스를 의미

Java에서 `실제 객체`는 `힙(heap) 메모리`에 저장되며 `참조 타입 변수`는 `스택 메모리`에 실제 객체들의 주소를 저장하여,
객체를 사용할 때마다 참조 변수에 저장된 객체의 주소를 불러와 사용하는 방식

이후 `Garbage Collector`가 돌면서 메모리를 해제한다.

![](/img/posts/reference.png)

<br>
<br>

## 원시 타입 vs 참조 타입

> Null 값을 담을 수 있는가?

`원시타입 : X`

`참조타입 : O`

<br>

> 제네릭 타입에 사용할 수 있는가? 

`원시타입 : X`

`참조타입 : O`

<br>

> 속도는 어떤 것이 더 빠른가?

`원시타입`

참조타입은 최소 2번의 메모리 접근이 필요

<br>
<br>
<br>
<br>

<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://velog.io/@wkdwoo/Primitive-type%EC%9B%90%EC%8B%9C%ED%83%80%EC%9E%85-vs.-Reference-type%EC%B0%B8%EC%A1%B0%ED%83%80%EC%9E%85>

<https://gyoogle.dev/blog/computer-language/Java/Primitive%20type%20&%20Reference%20type.html>
<div>
