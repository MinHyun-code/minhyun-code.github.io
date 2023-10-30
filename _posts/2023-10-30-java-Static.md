---
layout: post
title: "정적(static)"
subtitle: "기초 다지기"
category: "java"
date: 2023-10-30
background: '/img/posts/codeImg.jpg'
---

# static

static 키워드를 사용하여 `정적 필드`, `정적 메소드`를 만들 수 있다. (둘을 합쳐 `정적 멤버`라고도 한다.)

<br>

![static](/blog/img/posts/static.png)

<br> 

> 1. static 키워드를 통해 생성된 정적 멤버들은 Heap 영역이 아닌 Static 영역에 할당됨. <br>
>
> 2. 장점 : static 영역에 할당된 메모리는 모든 객체가 공유하여 하나의 멤버를 어디서든지 참조.
>
> 3. 단점 : Garbage Collector의 관리 영역 밖에 존재하기에, 프로그램의 종료시까지 메모리가 할당된 채로 존재.

<br>
<br>

## 정적(static) 멤버 선언

`static 사용 판단 기준은 공용으로 사용하는지 안하는지로 구분`

<br> 

```java
static int num = 0; // 타입 필드 = 초기값
public static void static_method() {}   // static 리턴 타입 메서드 {}
```

<br>
<br>

## 정적(static) 필드 사용 예시

```java
class Number {
    static int num = 0;     // 클래스 필드
    int num2 = 0;           // 인스턴스 필드
}

public class Static_ex {

    public static void main(String[] args) {

        Number number1 = new Number();
        Number number2 = new Number();

        number1.num++;
        number1.num2++;

        System.out.println(number2.num);
        System.out.println(number2.num2);
    }
}

// 결과
// 1
// 0
```

<br>

## 정적(static) 메서드 사용 예시

```java
class Name {
    static void print() {   //  정적 메서드
        System.out.println("내 이름은 홍길동입니다.");
    }
    void print2() { //  인스턴스 메소드
	    System.out.println("내 이름은 이순신입니다.");
    }

public class Static_ex {
	
    public static void main(String[] args) {
        Name.print(); //인스턴스를 생성하지 않아도 호출이 가능
            
        Name name = new Name(); //인스턴스 생성
        name.print2(); //인스턴스를 생성하여야만 호출이 가능
    }
}
```

<br>
<br>
<br> 

**참고 URL : <https://minhamina.tistory.com/127>**
