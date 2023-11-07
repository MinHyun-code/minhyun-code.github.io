---
layout: post
title: "이분 탐색 (Binary Search)"
subtitle: "자료구조"
category: "java"
date: 2023-10-30
background: '/img/posts/codeImg.jpg'
---

# 이분 탐색 (Binary Search) 

`정렬된 배열 또는 리스트에 적합한 고속 탐색 방법`

**배열의 중앙에 있는 값을 조사하여 탐색의 범위를 반으로 줄이는 방법을 반복적으로 사용하여 탐색**

<br>

> 데이터의 삽입이나 삭제가 빈번할 시에는 적합하지 않고, 주로 고정된 데이터에 대한 탐색에 적합

## 구현

1. array[low] ~ array[high] 일 경우, mid = (low + high)/2
2. 구하고자 하는 값을 array[mid] 와 비교
3. low > high가 될 때까지 반복

<br>

### 순환(재귀) 호출을 이용한 이진 탐색 구현

```java
public static int binarySearch(int[] arr, int key, int low, int high) {
    int mid;

    if(low <= high) {   
        mid = (low + high)/2;

        if(key == arr[mid]) {   // 탐색 성공
            return mid;
        } else if(key < arr[mid]) {
            return binarySearch(key, low, mid-1);
        } else if(key > arr[mid]) {
            return binarySearch(key, mid+1, high);
        }
    }

    return -1; // 탐색 실패
}
```

<br>

### ⭐⭐⭐반복을 이용한 이진 탐색 구현⭐⭐⭐

`반복이 재귀보다 호율적`

```java
public static int binarySearch(int[] arr, int key, int low, int high){

    while(low <= high) {
        mid = (low + high)/2;

        if(key == arr[mid]){
            return mid;
        } else if(key < arr[mid]) {
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    
    return -1; // 탐색 실패
}

```

<br>
<br>
<br>
<br>

## ⭐⭐⭐개수 찾기⭐⭐⭐

```java
private static int lowerBound(int[] arr, int key) {
	int lo = 0; 
	int hi = arr.length; 
 
	// lo가 hi랑 같아질 때 까지 반복
	while (lo < hi) {
 
		int mid = (lo + hi) / 2; // 중간위치를 구한다.
 
		/*
		 *  key 값이 중간 위치의 값보다 작거나 같을 경우
		 *  
		 *  (중복 원소에 대해 왼쪽으로 탐색하도록 상계를 내린다.)
		 */
		if (key <= arr[mid]) {
			hi = mid;
		}
 
		else {
			lo = mid + 1;
		}
 
	}
	return lo;
}
 
private static int upperBound(int[] arr, int key) {
	int lo = 0; 
	int hi = arr.length; 
 
	// lo가 hi랑 같아질 때 까지 반복
	while (lo < hi) {
 
		int mid = (lo + hi) / 2; // 중간위치를 구한다.
 
		// key값이 중간 위치의 값보다 작을 경우
		if (key < arr[mid]) {
			hi = mid;
		}
		// 중복원소의 경우 else에서 처리된다.
		else {
			lo = mid + 1;
		}
	}
	return lo;
}
```

<br>
<br>
<br> 

**참고 URL : <https://coding-factory.tistory.com/601>**
**참고 URL : <https://st-lab.tistory.com/267>**

