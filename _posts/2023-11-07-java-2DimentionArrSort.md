---
layout: post
title: "1,2차원 배열 정렬 (Comparator)"
subtitle: "알고리즘"
category: "java"
date: 2023-11-07
background: '/img/posts/2DimentionArrSort.png'
---

# 1,2차원 배열 정렬 (Comparator)

`Arrays.sort는 2차원 배열 정렬을 지원하지 않는다.`

<br>

```java
int[][] arr = new int[][]{ {5,40},{3,50},{1,30},{4,20},{2,10} };

// 1. Comparator 익명 클래스 구현
Arrays.sort(arr, new Comparator<int[]>() {
    @Override
    public int compare(int[] o1, int[] o2) {
        return o1[0]-o2[0];
        //return o2[0]-o1[0];
        //return o1[1]-o2[1];
        //return o2[1]-o1[1];
    }
});
```

<br>

- `o1[0]-o2[0]` : 첫번째 숫자 기준 오름차순 {1,30}{2,10}{3,50}{4,20}{5,40}
- `o2[0]-o1[0]` : 첫번째 숫자 기준 내림차순 {5,40}{4,20}{3,50}{2,10}{1,30}
- `o1[1]-o2[1]` : 두번째 숫자 기준 오름차순 {2,10}{4,20}{1,30}{5,40}{3,50}
- `o2[1]-o1[1]` : 두번째 숫자 기준 내림차순 {3,50}{5,40}{1,30}{4,20}{2,10}

<br>
<br>

```java
// 다중 조건 
int[][] arr2 = new int[][]{ {5,40},{3,50},{1,30},{4,20},{2,10},{6,40},{6,50},{6,10},{6,20},{6,30} };

Arrays.sort(arr2, new Comparator<int[]>() { 
    @Override
    public int compare(int[] o1, int[] o2) {
        return o1[0]!=o2[0] ? o1[0]-o2[0] : o1[1]-o2[1];
        //return o1[0]!=o2[0] ? o1[0]-o2[0] : o2[1]-o1[1];
    }
});
```

<br>

- `o1[0]!=o2[0] ? o1[0]-o2[0] : o1[1]-o2[1]` <br>
    첫번째 기준 오름차순 > 두번째 기준 오름차순 <br>
    {1,30}{2,10}{3,50}{4,20}{5,40}{6,10}{6,20}{6,30}{6,40}{6,50}
- `o1[0]!=o2[0] ? o1[0]-o2[0] : o2[1]-o1[1]` <br>
    첫번째 기준 오름차순 > 두번째 기준 내림차순 <br>
    {1,30}{2,10}{3,50}{4,20}{5,40}{6,50}{6,40}{6,30}{6,20}{6,10}

<br>
<br>
<br> 

**참고 URL : <https://ifuwanna.tistory.com/328>**

