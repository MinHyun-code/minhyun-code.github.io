---
layout: post
title: "promise"
subtitle: "비동기처리"
category: "javascript"
date: 2024-03-19
background: '/img/posts/codeImg.jpg'
---


# Promise

`비동기 처리`

<br>
<br>

### 언제 사용할까?

데이터를 받아오기 전에 화면에 데이터를 표시하려 하면 오류가 발생하거나 빈 화면이 나타남

이 현상을 해결하기 위해 사용

```javascript
$.get('url 주소/products/1', function(response) {
// ... 
});
```

<br>

### 사용방법

`new Promise()` 메서드 호출, 콜백함수 사용 가능(`resolve`, `reject`)

```javascript
function getData() {
    return new Promise(function(resolve, reject) {
        var data = 100;
        resolve(data);
    });
}

// resolve()의 결과 값 data를 resolvedData로 받음
getData().then(function(resolvedData) {
    console.log(resolvedData); // 100
});
```

<br>

### 프로미스의 3가지 상태

1. `Pending(대기)` : 비동기 처리 로직이 아직 완료되지 않은 상태
2. `Fulfilled(이행)` : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
3. `Rejected(실패)` : 비동기 처리가 실패하거나 오류가 발생한 상태

<br>

![alt text](/img/posts/promise.svg)
프로미스 처리 흐름 - 출처 : MDN

<br>

### 에러처리 방법

`catch 사용 !!`

```javascript
// catch()로 오류를 감지하는 코드
function getData() {
    return new Promise(function(resolve, reject) {
        resolve('hi');
    });
}

getData().then(function(result) {
    console.log(result); // hi
    throw new Error("Error in then()");
}).catch(function(err) {
    console.log('then error : ', err); // then error :  Error: Error in then()
});
```


<br>
<br>
<br>

<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://joshua1988.github.io/web-development/javascript/promise-for-beginners/>
<div>
