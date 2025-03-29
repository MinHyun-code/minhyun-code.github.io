---
layout: post
title: "Spring IOC/DI"
subtitle: "Spring 핵심 요소 IOC/DI 정리"
category: "java"
date: 2023-10-27
background: '/img/posts/ioc di main.png'
---


# IoC (Inversion of Control)

객체의 생성부터 생명주기 관리를 프레임워크(컨테이너)가 도맡아서 한다.

`= 제어권이 개발자에서 컨테이너로 넘어가게 되는 현상`

<br>
<br>

### - 기존 객체 생성 과정

1. 객체 생성
2. 의존성 객체 생성 -> 클래스 내부에서 생성
3. 의존성 객체 메소드 호출

<br>

### - 스프링 객체 생성 과정

1. 객체 생성
2. 의존성 객체 주입 -> 제어권을 스프링에게 위임하여 스프링이 만들어놓은 객체를 주입
3. 의존성 객체 메소드 호출

`스프링이 실행될 때 모든 의존성 객체를 다 만들어주고 필요한 곳에 주입시켜 준다.`

<br>
<br>

# DI (Dependency Injection)

객체를 직접 생성하는 것이 아니라 외부에서 생성한 후 주입시켜주는 방식

`모듈 간 결합도가 낮아지고 유연성이 높아진다.`

<br>
<br>

## DI 유형

### 1. 수정자 주입 (Setter Injection)

의존성을 입력 받는 setter 메서드를 만들고 이를 통해서 의존성을 주입한다.

```java
@Component
public class SampleController {
   private SampleRepository sampleRepository;
   @Autowired // 있어도 되고, 없어도 됨
   public void setSampleRepository(SampleRepository sampleRepository) {
       this.sampleRepository = sampleRepository;
   }
}
```

<br>

### 2. ⭐⭐⭐ 생성자 주입 (Contructor Injection) ⭐⭐⭐

Spring Framework Reference에서 권장하는 방법 

``` java
@Component
public class SampleController {
    // final을 사용할 수 있다.
   private final SampleRepository sampleRepository;
   public SampleController(SampleRepository sampleRepository) {
       this.sampleRepository = sampleRepository;
   }
}
```

<br>

### 3. 필드 주입 (Field Injection)

변수 선언부에 `@Autowired` 어노테이션을 붙인다.

``` java
@Component
public class SampleController {
    @Autowired
    private SampleRepository sampleRepository;
}
```

<br>
<br>

## 생성자 주입을 권장하는 이유

<br>

**1. 구동 시 순환 참조 확인 가능**

- (생성자)와 (필드, 수정자) 간의 `의존성 주입하는 시점`이 다르다.
- 필드, 수정자 주입의 경우, 빈 객체를 먼저 생성한 뒤에 의존성을 주입 <br> -> `구동 시 순환 참조 확인 불가능`
- 생성자 주입의 경우, 빈 객체를 생성하는 시점에 생성자의 파라미터 빈 객체를 찾아 먼저 주입한 뒤에 주입받은 빈 객체를 이용하여 생성  <br>-> `구동 시 순환 참조 확인 가능`

<br>

> **순환 참조 문제**
> <br><br>
> A클래스가  B클래스의 Bean을 주입받고, B클래스가 A클래스의 Bean을 주입받는 상황

<br>
<br>

**2. final 키워드 사용 가능**

- 필드, 수정자 주입의 경우, 예기치 못한 상황으로 빈 객체가 변경될 수 있다.
- 생성자 주입의 경우, `final`을 사용 <br>-> null이 아님을 보장할 수 있고 초기화된 객체는 변경할 수 없다.

**3. Lombok의 어노테이션 `@RequiredArgsConstructor`을 활용하여 간단히 작성**

```java
@Component
public class Example1 {

    private final Example2 example2;

    public Example1(Example2 example2) {
        this.example2 = example2;
    }

    public void playMusic() {
        example2.playGame();
    }
}

// Lombok 어노테이션을 통한 의존성 주입
@Component
@RequiredArgsConstructor
public class Example2 {

    private final Example1 example1;

    public void playGame() {
        example1.playMusic();
    }
}
```

<br>
<br>

**3. 테스트 코드를 작성하기 쉽다.**

- 필드 주입의 경우, 순수한 자바 코드로 단위 테스트를 작성하는 것은 불가능하다.
- 예를 들어, 아래와 같은 코드가 있다고 해보자.

```java
@Service
public class ExampleService {

    @Autowired
    private ExampleRepository exampleRepository;

    public void save(int seq) {
    	exampleRepository.save(seq);
    }
}

public class ExampleTest {
	
    @Test
    public void test() {
    	ExampleService exampleService = new ExampleService();
        exampleService.save(1);
    }
}
```

**결과**
1. Spring과 같은 DI 프레임워크 위에서 동작하지 않기 때문에 의존성 주입이 되지 않을 것이다.
2. 그렇다면 exampleService = null, exampleService.add(1)은 NPE를 발생시킬 것이다.
3. 수정자 주입의 경우, <br>`SOLID(객체 지향 설계 원칙)`의 `OCP(개방-폐쇄 원칙, Open-Closed Principle)`을 위반하게 된다.

<br>
<br>

**생성자 주입 방식을 이용하면 아래와 같이 작성할 수 있다.**

```java
@Service
public class ExampleService {

    private final ExampleRepository exampleRepository;
    
    public ExampleService (ExampleRepository exampleRepository) {
    	this.exampleRepository = exampleRepository;
    }

    public void save(int seq) {
    	exampleRepository.save(seq);
    }
}

public class ExampleTest {
	
    @Test
    public void test() {
    	ExampleRepository exampleRepository = new ExampleRepository();
    	ExampleService exampleService = new ExampleService(exampleRepository);
        exampleService.save(1);
    }
}
```