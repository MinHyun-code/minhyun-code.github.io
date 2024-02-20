---
layout: post
title: "var, let, const 차이"
subtitle: "기초다지기"
category: "javascript"
date: 2024-02-07
background: '/img/posts/codeImg.jpg'
---

## 변수 선언 방식

<br>

### `var : 중복 선언 가능`

```javascript
var name = 'javascript';
console.log(name); // javascript

var name = 'react';
console.log(name); // react
```

- var로 선언한 변수는 동일한 이름으로 여러번 중복 선언 가능
- 마지막에 할당된 값이 변수에 저장됨
- 유연하게 사용하여 편리할수는 있지만, 문제 발생 시 파악하기 어려움
- 이를 보완하기 위해 ES6부터 추가된 변수 선언 방식이 `let`, `const`

<br>
<br>

### `let : 중복 선언 불가능, 재할당 가능`

```javascript
let name = 'javascript';
console.log(name);  // javascript

let name = 'react';
// Uncaught SyntaxError: Identifier 'name' has already been declared

name = 'vue';
console.log(name);  // vue
```

- var와 다르게 중복 선언 시, 이미 선언되었다는 오류 메세지 출력
- 값을 재할당은 할 수 있음

<br>
<br>

### `const : 중복 선언 불가능, 재할당 불가능`

```javascript
const name = 'javascript';
console.log(name);   // javascript

const name = 'react';
// Uncaught SyntaxError: Identifier 'name' has already been declared

name = 'vue';
console.log(name);
// Uncaught TypeError: Assignment to constant variable
```

- 값이 불변하는 것이 아니라 재할당을 불가

```javascript
function func() {
  const list = ["A", "B", "C"];
  
  list = "D";
  console.log(list);
  // TypeError: Assignment to constant variable

  list.push("D");
  console.log(list);
  // ["A","B","C","D"]
}
```

- 위처럼 값을 변경하지는 못하지만, 배열과 오브젝트의 값을 변경하는 것은 가능함


<br>
<br>

> 최적의 사용 방법
>
> `const`를 기본으로 사용하되, 재할당이 필요한 경우 `let` 사용

<br>
<br>

## 스코프 (Scope) - 유효한 참조 범위

<br>

### var : 함수 레벨 스코프 (function-level scope)

```javascript
function func() {
  if(true) {
    var a = 5;
    console.log(a); // 5
  }
  console.log(a);   // 5
}

func(); // 5 
console.log(a); // ReferenceError: a is not defined
```

- 함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조될 수 없음
- 함수 내부 : `지역 변수`
- 함수 외부 : `전역 변수`

<br>
<br>

### let, const : 블록 레벨 스코프 (block-level scope)

```javascript
function func() {
  if(true) {
    let a = 5;
    console.log(a); // 5
  }
  console.log(a); // ReferenceError: a is not defined
}

console.log(a); // ReferenceError: a is not defined
```

- 함수, if문, for문, while문, try/catch문 등의 모든 코드 블럭 내부에서 선언된 변수는 코드 블럭 내에서만 유효하며, 코드 블럭 외부에서는 참조 불가능
- 코드 블럭 내부에서 선언한 변수는 지역 변수로 취급

<br>
<br>

## 호이스팅 (Hoisting)

- 호이스팅이란 함수 내부에 있는 선언들을 모두 끌어올려 해당 함수 유효 범위의 최상단에 선언하는 것을 뜻한다.
`(간단하게 미리 선언문을 실행한다고 이해)`

### var, 함수 선언문 : 호이스팅이 발생

```javascript
// 변수 호이스팅
console.log(a); // undefined

var a = 5;
console.log(a); // 5

// 함수 호이스팅
foo();  // foo

function foo() {
  console.log("foo");
}
```

- 변수가 선언되기 전에 참조되었음에도 에러가 발생하지 않음. 
- 함수 선언문도 선언 전에 호출하엿지만 에러가 발생하지 않음.

`코드 실행 전에 자바스크립트 내부에서 미리 변수를 선언 -> undefined로 초기화, 함수도 동일`

<br>

### let, const, 함수 표현식 : 호이스팅이 발생하지만, 다른 방식으로 작동됨

```javascript
// 변수 호이스팅
console.log(a); // ReferenceError: a is not defined

let a = 5;
console.log(a); // 5

// 함수 호이스팅
foo();  // error

var foo() = function() {
  console.log('foo');
}
```

- 호이스팅은 발생하지만, 값을 참조할 수 없기 때문에 동작하지 않는 것처럼 보임

`자바스크립트 내부에서 코드 실행 전에 변수 선언만, 초기화는 X`

`초기화는 실행 과정에서 변수 선언문을 만났을 때 진행`


<br> 
<br> 
<br>


<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://80000coding.oopy.io/e1721710-536f-43f2-823b-663389f5fbfa>
<div>
