---
layout: post
title: "기초"
subtitle: "기초다지기"
category: "typescript"
date: 2024-02-05
background: '/img/posts/codeImg.jpg'
---

# Typescript

`Javascript의 업그레이드 버전 - 타입부분`

<br>
<br>

## 사용이유

1. 정확한 에러 메세지
2. 타입을 엄격하게 검사

<br>
<br>

## .ts 파일 = 타입스크립트 파일

tsconfig.json 생성 후 아래 내용 작성

```typescript
{   
  "compilerOptions" : {     
    "target": "es5",     
    "module": "commonjs",  
  } 
}
```

<br>

Typescript 파일을 Javascript 파일로 변환 후 사용 `명령어: tsc -w (자동 변환 시켜줌)`

<br>
<br>

## 타입 지정 방법

```typescript
// 문자
let 이름:string = 'kim';

// 문자 또는 숫자 (= 유니온 타입)
let 이름:string | num = 123;

// 배열
let 배열:string[] = ['kim', 'park'];

// 오브젝트
let 오브젝트:{name?: string} = {name: 'kim'};   // ?: 속성이 들어올지 안들어올지 불확실함


// 미리 타입을 지정하여 가져올수도 있음
type Name = string | number;
let 이름 :Name = 123;


// 함수에 타입 지정
function 함수(x:number) :number {   // 뒤에 있는 타입은 리턴의 타입
    return x * 2
}

// tuple 타입 (array 형태에 사용 가능)
type Member = [number, boolean];
let john:Member = [123, true];

// object 타입에 속성이 많을 경우
type Member = {
    [key :string] : string,
}

let john : Member = {name: 'kim', age: '123'};
```

<br> 
<br> 
<br>


