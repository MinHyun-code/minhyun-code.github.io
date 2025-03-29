---
layout: post
title: "인덱스란?"
subtitle: "index"
category: "database"
date: 2024-04-05
background: '/img/posts/index main.png'
---

# 인덱스란?

`추가적인 쓰기 작업과 저장 공간을 활용하여 데이터베이스 테이블의 검색 속도를 향상시키기 위한 자료구조`

<br>

![](/img/posts/index.png)

<br>

## 인덱스 관리

DBMS는 `index`를 항상 최신 정렬된 상태로 유지해야 빠른 값을 찾을 수 있다.

따라서, 인덱스가 적용된 컬럼에 `INSERT`, `UPDATE`, `DELETE`가 수행된다면 각각 다음과 같은 연산을 추가적으로 해주어야 한다.

> 1. `INSERT` : 새로운 데이터에 인덱스를 추가
> 2. `DELETE` : 삭제하는 데이터의 인덱스를 사용하지 않는다는 작업을 진행
> 3. `UPDATE` : 기존의 인덱스를 사용하지 않음 처리하고, 갱신된 데이터에 대해 인덱스를 추가

<br> 
<br> 

## 인덱스 장단점

장점
- 테이블을 조회하는 속도와 그에 따른 성능을 향상시킬 수 있다.
- 전반적인 시스템의 부하를 줄일 수 있다.

단점
- 인덱스를 관리하기 위해 DB의 약 10%에 해당하는 저장공간이 필요하다.
- 인덱스를 관리하기 위한 추가 작업이 필요하다.
- 인덱스를 잘못 사용할 경우, 오히려 성능이 저하될 수 있다.

<br>

> DELETE와 UPDATE 시, 기존 인덱스는 사용하지 않음으로 처리할 때 실제 데이터보다 Index가 더욱 많아져 성능 저하가 발생될 수 있다.

<br>
<br>

## 인덱스를 사용하면 좋은 경우

- 규모가 작지 않은 테이블
- INSERT, UPDATE, DELETE가 자주 발생하지 않는 컬럼
- JOIN이나 WHERE 또는 ORDER BY에 자주 사용되는 컬럼
- 데이터의 중복도가 낮은 컬럼

<br>
<br>

## 자료구조

<br>

### 해시 테이블

`(key, Value)로 데이터를 저장` `빠른 데이터 검색 유용` `시간복잡도 : O(1)`

`등호 연산`에만 특화되어 있어 부등호 연산이 자주 사용되는 데이터베이스 검색에는 적합하지 않다.

ex. (데이터=컬럼의 값, 데이터의 위치)

<br>
<br>

### B+ Tree ⭐

`자식 노드가 2개 이상인 B-Tree를 개선시킨 자료구조` `시간복잡도 : O(log2n)`

**B Tree와 다른 특성**

- 리프 노드(데이터)만 인덱스와 함께 데이터(Value)를 가지고 있고, 나머지 노드(인덱스 노드)들은 데이터를 위한 인덱스(Key)만을 갖는다.
- 리프 노드들은 LinkedList로 연결되어 있다.
- 데이터 노드의 크기는 인덱스 노드의 크기와 같지 않아도 된다.

<br>

[**B Tree 알아보기**](https://minhyun-code.github.io/database/2024/04/05/database-B-Tree.html)

<br>
<br>

<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://mangkyu.tistory.com/96/>
<div>
