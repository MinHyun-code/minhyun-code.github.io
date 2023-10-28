---
layout: post
title: "Queue"
subtitle: "자료구조"
category: "java"
date: 2023-10-28
background: '/img/posts/codeImg.jpg'
---

# Queue 

데이터를 일시적으로 쌓아두기 위한 `자료구조`로 `FIFO`의 형태

<> 반대되는 자료구조는 `Stack`

> FIFO (First In First Out) : 먼저 들어온 데이터가 가장 먼저 나가는 구조

<br>
<br>

## Queue의 특징

1. 먼저 들어간 자료가 먼저 나오는 `FIFO` 구조
2. 큐는 한 쪽 끝은 `front`로 정하여 `삭제 연산`만 수행
3. 다른 한 쪽 끝은 `rear`로 정하여 `삽입 연산`만 수행
4. 그래프의 넓이 우선 탐색(BFS)에서 사용
5. 컴퓨터 버퍼에서 주로 사용 <br>
    마구 입력이 되었으나 처리를 하지 못할 때, 버퍼(큐)를 만들어 대기 시킴

<br>
<br>

## Queue 사용법

### Queue 선언

```java
import java.util.LinkedList;
import java.util.Queue;

Queue<Integer> queue = new LinkedList<>();
Queue<String> queue = new LinkedList<>();
```

**⭐`LinkedList`**와 함께 사용하여야 한다.⭐

<br>

### Queue 값 추가

```java
Queue<Integer> queue = new LinkedList<>();

Queue.add(1);   // 1 추가
Queue.add(2);   // 2 추가
Queue.offer(3); // 3 추가
```

**`add, offer`**를 사용하여 값 추가한다.

<br>

### Queue 값 삭제

```java
Queue<Integer> queue = new LinkedList<>();

queue.offer(1); // 1 추가
queue.offer(2); // 2 추가
queue.offer(3); // 3 추가
queue.poll();   // queue에 첫번째 값을 반환하고 제거. 비어있다면 null
queue.remove(); // queue 첫번째 값 삭제
queue.clear();  // queue 초기화
```
**`poll, remove, clear`**상황에 맞게 사용하여 값 제거한다.

<br>

### Queue에서 가장 먼저 들어간 값 출력

```java
Queue<Integer> queue = new LinkedList<>();

queue.offer(1);
queue.offer(2);
queue.offer(3);
queue.peek();       // 첫번째 값 참조
```

**`peek`**을 사용하여 첫번째 값을 가져온다. 

<br>
<br>
<br> 

**참고 URL : <https://coding-factory.tistory.com/602>**
