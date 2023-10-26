---
layout: post
title: "마크다운 문법 정리"
subtitle: "github blog 시작 !!"
date: 2023-10-25
background: '/img/posts/markdown.jpg'
---

## 중첩 구조

```
- 1
  - 2
    - 3
```

- 1
  - 2
    - 3

## 순서

```
- 순서가
  * 없는
    + 목록 
  * 순서가
- 없어용

1. 순서가
2. 있는  
   1. 목록
      - 하나
      - 둘
   2. 목록
       - 하나
       - 둘
3. 목록   
```
- 순서가
  * 없는
    + 목록 
  * 순서가
- 없어용

1. 순서가
2. 있는  
   1. 목록
      - 하나
      - 둘
   2. 목록
       - 하나
       - 둘
3. 목록   

<br>
<br>

## 헤더

```
# h1
## h2
### h3
#### h4
##### h5
###### h6
```

# h1
## h2
### h3
#### h4
##### h5
###### h6

<br>

## 텍스트

<br>

### 1. 굵기

```
**텍스트**
```

**텍스트**

<br>

### 2. 기울기

```
*텍스트입니다*
```

*텍스트입니다*

<br>

### 3. 취소선

```
~~취소된 텍스트입니다~~
```

~~취소된 텍스트입니다~~

<br>

### 4. 밑줄

```
<u>밑줄 있는 텍스트입니다</u>
```

<u>밑줄 있는 텍스트입니다</u>

<br>

### 5. 색상
```
<span style="color:red">빨간</span> 글씨입니다.
```

<span style="color:red">빨간</span> 글씨입니다.

<br>
<br>

## 인라인 코드

```
이런게 바로 `인라인 코드`입니다.
```

<br>

이런게 바로 `인라인 코드`입니다.

<br>
<br>

## 코드

```c++
#include <iostream>
using namespace std;

int main()
{
cout « “Hello World !” « endl; // 안녕!
}
```

<br>
<br>

## URL

```
<https://www.google.com>
[구글 홈페이지](https://www.google.com)
```

<br>

<https://www.google.com>

[구글 홈페이지](https://www.google.com)

<br>



## 인용문

```
> 이건 인용문이에요.
```

> 이건 인용문이에요.

<br>
<br>

## 체크박스

```
- [ ] 체크 안됨
- [X] 체크 됨
```

- [ ] 체크 안됨
- [X] 체크 됨

<br>
<br>

## 구분선
```
---
```
---

<br>
<br>

## 테이블

```
|**제목**|레이팅|감상평|
|:---:|:---:|:---:|
|복수는 나의 것|⭐⭐⭐⭐⭐|내가|
|올드 보이|⭐⭐⭐⭐⭐|좋아하는|
|친절한 금자씨|⭐⭐⭐⭐⭐|박찬욱 영화!|
```

|**제목**|레이팅|감상평|
|:---:|:---:|:---:|
|복수는 나의 것|⭐⭐⭐⭐⭐|내가|
|올드 보이|⭐⭐⭐⭐⭐|좋아하는|
|친절한 금자씨|⭐⭐⭐⭐⭐|박찬욱 영화!|

<br>
<br>

## 토글

```
<details>
<summary>여기를 눌러주세요</summary>
<div markdown="1">       

⭐숨겨진 내용⭐

</div>
</details>
```
<details>
<summary>여기를 눌러주세요</summary>
<div markdown="1">       

⭐숨겨진 내용⭐

</div>
</details>

<br>
<br>

## 버튼

```
<a href="#" class="btn--success">Success Button</a>
[Default Button](#){: .btn .btn--primary }
```
<a href="#" class="btn--success">Success Button</a>

[Default Button](#){: .btn .btn--primary }
