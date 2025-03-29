---
layout: post
title: "DP - 동적 계획법"
subtitle: "Dynamic Programming"
category: "algorithm"
date: 2024-01-12
background: '/img/posts/dp main.png'
---

# 동적 계획법

중복되는 호출의 결과값을 메모리 영역에 저장하여 이후 사용할 경우, 호출하지 않고 저장된 값을 참조하여 사용

<br>
<br>
<br>

## DP가 성립할 조건

1.`최적 부분 구조 (Optimal Substructure)`

- 상위 문제를 하위 문제로 나눌 수 있으며 하위 문제의 답을 모아서 상위 문제를 해결할 수 있다.

2.`중복되는 부분 문제 (Overlapping Subproblem)`

- 동일한 작은 문제를 반복적으로 해결해야 한다.


<br>
<br>
<br>

## 구현 방법 (Memoization)

```java
// 일반 재귀 함수
// 중복된 계산을 반복해서 하게 된다. 시간복잡도 O(2^n)으로 x의 수가 커질수록 복잡도가 엄청나게 커짐
static int fibo(int x) {
   if( x ==1 || x==2) return 1;
   return fibo(x-1) + fibo(x-2);
}


// Memoization 
// 하위 문제의 결과 값을 dp[]배열에 저장해놓고 필요할 때마다 계산된 값을 호출
static int fibo(int x) {
   if( x ==1 || x==2) return 1;
   if(dp[x] != 0) return dp[x];
   dp[x] = fibo(x-1) + fibo(x-2);
   return dp[x];
}
```


<br> 
<br> 
<br>

**참고 URL : <https://loosie.tistory.com/150#>**
