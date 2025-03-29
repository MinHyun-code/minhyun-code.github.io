---
layout: post
title: "연관관계"
subtitle: "Relationship"
category: "jpa"
date: 2024-01-29
background: '/img/posts/jpa relationship.png'
---

# 연관관계

> 객체 - 참조 (객체 그래프 탐색, JPQL)
> 
> 관계형 DB - 외래키 (JOIN)

<br>
<br>

객체에서는 관계형 DB의 외래키처럼 양방향으로 연관관계를 설정할 수 없다.

따라서, 단방향 2개로 구현.

<br>
<br>


### 구현 방법

`User(Many) <-> Board(One) : 일대다 관계`

```java
    // User.java
	@OneToMany(mappedBy = "userId")
	private Set<Board> board = new LinkedHashSet<>();


    // Board.java
    @ManyToOne
    @JoinColumn(name="user_id")
	private User userId;
```

`mappedBy`는 주인이 아닌 필드에 사용

<br>

<hr>

> 주인 
> 
> 외래키가 있는 곳으로, 주인 필드에 값을 넣지 않고 반대 필드에 값을 넣을 경우, NULL로 인식

<br>

주인의 값만 넣어도 JPA는 잘 작동하지만, 순수한 객체 연관관계에서는 작동하지 않는다. 

따라서, 주인뿐만 아니라 반대편의 값도 넣어줘야 안전한 코드라고 할 수 있다.

<br>
<br>

### 연관관계 편의 메소드

`위 작업을 조금 더 편리하게 작업하기 위한 메소드`

```java
	public void setUserId(User userId) {
		this.userId = userId;
		userId.getBoard().add(this);
	}
```

<br>
<br>
<br> 

참조 : JPA프로그래밍 책 - 저자: 김영한

