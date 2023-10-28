---
layout: post
title: "Stack"
subtitle: "자료구조"
category: "java"
date: 2023-10-29
background: '/img/posts/codeImg.jpg'
---

# Stack 

데이터를 일시적으로 쌓아두기 위한 `자료구조`로 `LIFO`의 형태

<> 반대되는 자료구조는 `Queue`

> LIFO (Last In First Out) : 먼저 들어온 데이터가 가장 나중에 나가는 구조

<br>
<br>

## Stack의 특징

1. 먼저 들어간 자료가 나중에 나오는 `LIFO` 구조
2. 시스템 해킹에서 버퍼오버플로우 취약점을 이용한 공격을 할 때 스택 메모리의 영역에서 함
3. 인터럽트 처리, 수식의 계산, 서브루틴의 복귀 번지 저장 등에 쓰임
4. 그래프의 깊이 우선 탐색(DFS)에서 사용
5. 재귀적 함수를 호출할 때 사용

<br>
<br>

## Stack 사용법

### Stack 선언

```java
import java.util.Stack;

Stack<Integer> stack = new Stack<>();
Stack<String> stack = new Stack<>();
```

<br>

### Stack 값 추가

```java
Stack<Integer> stack = new Stack<>();

stack.push(1);   // 1 추가
stack.push(2);   // 2 추가
stack.push(3);   // 3 추가
```

**`push`**를 사용하여 값 추가한다.

<br>

### Stack 값 삭제

```java
Stack<Integer> stack = new Stack<>();

stack.push(1);   // 1 추가
stack.push(2);   // 2 추가
stack.push(3);   // 3 추가
stack.pop();     // stack에 값 제거
stack.clear();   // stack의 전체 값 제거 (초기화)
```
**`pop, clear`**상황에 맞게 사용하여 값 제거한다.

<br>

### Stack에서 가장 먼저 들어간 값 출력

```java
Stack<Integer> stack = new Stack<>(); //int형 스택 선언

stack.push(1);     // stack에 값 1 추가
stack.push(2);     // stack에 값 2 추가
stack.push(3);     // stack에 값 3 추가
stack.peek();      // stack의 가장 상단의 값 출력
```

**`peek`**을 사용하여 첫번째 값을 가져온다. 

<br>
<br>
<br> 

**참고 URL : <https://coding-factory.tistory.com/601>**
