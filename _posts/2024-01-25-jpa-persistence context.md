---
layout: post
title: "영속성 컨텍스트"
subtitle: "Persistence context"
category: "jpa"
date: 2024-01-25
background: '/img/posts/Persistence context.png'
---

# 영속성 컨텍스트 (persistence context)

`엔티티를 영구 저장하는 환경`

엔티티 매니저를 생성할 때 만들어지며, 엔티티 매니저를 통해 관리할 수 있다.

<br>

![aspect](/img/posts/JPA_1.png)

<br>

```java
    // 엔티티매니저팩토리 생성 (비용이 아주 많이 듦)
    EntityManagerFactory emf = Persistence.createEntityManagerFactory("jpabook");

    // 엔티티매니저 생성 (비용이 거의 안듦)
    EntityManager em = emf.createEntityManager();
```

<br>

> EntityManagerFactory (여러 스레드 동시에 접근 가능)
> 
> -- `META-INF/persistance.xml` 정보를 바탕으로 생성됨
> 
> 2 . EntityManager (여러 스레드 동시에 접근하면 `동시성 문제 발생`)
> 
> -- EntityManagerFactory를 통해 생성됨

<br>

## 장점

<br>

### 1차 캐시

DB의 기본키를 key로한 Map

```java
    // 엔티티 생성 (비영속)
    Member member = new Member();
    member.setId("memberId1");
    member.setUsername("회원1");

    // 엔티티 영속
    em.persist(member);
```

아직 DB에 저장되지 않고 1차 캐시에 담겨져 있다.

`em.find()`를 호출하면 메모리에 있는 1차 캐시에서 조회 `(동일성 보장)`

만약 없으면 DB에서 조회 후 1차 캐시에 엔티티 영속

<br>
<br>

### 쓰기 지연

```java
    transaction.begin();    // 트랜잭션 시작

    em.persist(member1);    // INSERT
    em.persist(member2);    // INSERT

    // 아직 DB에 쿼리를 전달하지 않고 쓰기지연 SQL 저장소에 담아둔다.

    transaction.commit();   // 저장소에 담아둔 SQL을 DB에 전달, 영속성 컨텍스트 flush
```
<br>
<br>

### 변경 감지 (삭제도 동일)

- SQL로 엔티티를 수정할 경우, 필드가 추가될 때마다 모든 UPDATE SQL을 수정해줘야한다. 이것을 해결하기 위해 `변경감지`를 사용

- 변경감지는 모든 필드를 업데이트 해주므로, 30개 이상의 필드를 가진 엔티티일 경우는 UPDATE SQL을 생성하는 전략을 활용하면 됨.

- 수정된 데이터만 동적으로 UPDATE SQL을 생성해주기 위해서는 엔티티 클래스에서 `org.hibernate.annotations.DynamicUpdate`를 사용하면 된다.

- `em.remove()`를 호출하는 순간 영속성 컨텍스트에서 삭제, DB에 쿼리는 전달 X

<br>

**순서**
 
 1. 트랜잭션을 커밋 - 엔티티 매니저에서 flush() 호출
 2. 엔티티와 스냅샷(최초 상태)을 비교해서 변경된 엔티티를 찾음
 3. 존재한다면, 수정 쿼리를 생성하여 쓰기 지연 SQL 저장소에 저장
 4. 쓰기 지연 저장소의 SQL을 데이터베이스에 보냄
 5. 데이터베이스 트랜잭션 커밋

<br>
<br>

## flush() 방법

 1. `em.flush()` 직접 호출
 2. 트랜잭션 커밋 시 자동 호출
 3. JPQL 쿼리 실행 시 자동 호출

<br>
<br>

## 영속 - 준영속 상태 변환 방법
 
 준영속 = 영속성 컨텍스트에서 관리 X

 1. `em.detach(entity)` - 특정 엔티티만 준영속 상태로 변환 
 2. `em.clear()` - 영속성 컨텍스트 초기화
 3. `em.close()` - 영속성 컨텍스트 종료

<br>
<br>
<br> 

참조 : JPA프로그래밍 책 - 저자: 김영한

