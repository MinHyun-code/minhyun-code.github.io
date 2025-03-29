---
layout: post
title: "@Builder"
subtitle: "lombok"
category: "java"
date: 2024-07-24
background: '/img/posts/builder.png'
---

## Builder 패턴

`객체 생성을 위한 방법` `필드 순서 상관 X`

<br>

### lombok @Builder 미사용

```java
public class Test{
    private Integer number;
    private String str;
    
    public static class Builder{
        private Integer number;
        private String str;
        
        public Builder number(Integer number){
            this.number = number;
            return number;
        }
        
        public Builder str(String str){
            this.str = str;
            return this;
        }
        
        public Test build(){
            return new Test(number, str);
        }
    }
}

public class TestMain{
   @Test
   void test1(){
       Test test = Test.builder()
                       .number(1)
                       .str("test")
                       .build();
       System.out.println("output : " + test.getNumber() + " " + test.getStr());
       
       Test test2 = Test.builder()
                       .str("test2")
                       .number(2)
                       .build();
       System.out.println("output : " + test2.getNumber() + " " + test2.getStr());
   }
}
```

> output : 1 test
> 
> output : 2 test2

<br>

### lombok @Builder 사용

```java
@Builder
@Getter
public class Test{
    private Integer number;
    private String str;
}

public class TestMain{
   @Test
   void test1(){
       Test test = Test.builder()
                       .number(1)
                       .str("test")
                       .build();
       System.out.println("output : " + test.getNumber() + " " + test.getStr());
   }
}
```
<br>
<br>

### 기본값 초기화

Builer를 사용하여 생성 시 값을 지정하지 않으면 타입에 따라 0, null, false 값이 할당
```java
// 아래와 같이 변수에 값을 지정하여도 default값으로 셋팅되지 않음
private String str = "default";

// Builder 디폴트 설정
@Builder.Default
private String str=  "default";

```

<br>
<br>
<br>
<br>

<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://velog.io/@kshired/Spring-Lombok-Builder-%EA%B8%B0%EB%B3%B8%EA%B0%92%EC%97%90-%EA%B4%80%ED%95%98%EC%97%AC>
<div>
