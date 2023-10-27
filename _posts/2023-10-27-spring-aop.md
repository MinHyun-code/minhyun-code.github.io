---
layout: post
title: "Spring AOP"
subtitle: "Spring 핵심 요소 AOP 정리"
category: "java"
date: 2023-10-27
background: '/img/posts/spring.png'
---

# AOP (Aspect Oriented Programming)

`관점 지향 프로그래밍` : 핵심적인 관점, 부가적인 관점으로 나누고 각각 모듈화

<br>

반복해서 쓰는 코드들을 발견할 수 있는데 이 부분이 `흩어진 관심사(Crosscutting Concerns)`라 부른다.

![aspect](/blog/img/posts/aspect.png)

1. 흩어진 관심사를 `Aspect`로 모듈화하고 
2. 핵심적인 비즈니스 로직에서 `분리하여 재사용`하겠다는 것이 AOP의 취지

<br> 

## AOP의 주요 개념

- **Aspect** : 위에서 설명한 흩어진 관심사를 모듈화 한 것. 
    <br>(주로 부가기능을 모듈화)

- **Target** : Aspect를 적용하는 곳 
    <br>(클래스, 메서드 등)

- **Advice** : 실질적으로 어떤 일을 해야할 지에 대한 것. 
    <br>(실질적인 부가기능을 담은 구현체)

- **JointPoint** : Advice가 적용될 위치, 끼어들 수 있는 지점. 
    <br>(메서드 진입 지점, 생성자 호출 지점, 필드에서 값을 꺼내오는 지점 등)

<br>

## 스프링 AOP 특징

- `프록시 패턴 기반의 AOP 구현체`, 프록시 객체를 쓰는 이유는 접근 제어 및 부가기능을 추가하기 위해서임

- 스프링 빈에만 AOP 적용 가능

- 모든 AOP 기능을 제공하는 것이 아닌 스프링 IoC와 연동하여 애플리케이션에서 가장 흔한 문제 해결 지원 목적

<br>
<br>
<br> 

**참고 URL : <https://engkimbs.tistory.com/entry/%EC%8A%A4%ED%94%84%EB%A7%81AOP>**

<br>