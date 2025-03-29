---
layout: post
title: "Deque (덱)"
subtitle: "자료구조"
category: "java"
date: 2023-10-30
background: '/img/posts/deque main.png'
---

# Deque (Double-Ended Queue)

양쪽으로 엘리먼트를 삽입, 삭제를 수행할 수 있는 자료구조를 의미

어떤 쪽으로 입력하고 출력하냐에 `따라 스택, 큐`로 사용 가능

Queue와 동일하게 `LinkedList`로 구현

<br>

> 한쪽으로 입력 가능하도록 설정한 덱을 scroll
>
> 한쪽으로 출력 가능하도록 설정한 덱을 shelf

<br>
<br>

## 선언

```java
Deque<Integer> deque = new LinkedList<Integer>();   // 선언
```

<br>

## 메서드 (많이 사용하는 것만 정리)

`대부분의 메서드는 first, last로 위치 선정`

삽입 : add, offer

삭제 : remove

리턴, 삭제O : poll

리턴, 삭제X : peek, get

<br>
<br>
<br> 

**참고 URL : <https://soft.plusblog.co.kr/24>**
