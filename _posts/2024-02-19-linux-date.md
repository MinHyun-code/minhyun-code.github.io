---
layout: post
title: "리눅스(linux) UTC, KST 수정"
subtitle: "Scheduler 작동 X"
category: "linux"
date: 2024-02-19
background: '/img/posts/codeImg.jpg'
---

## 현상

<br>

매일 저녁 6시로 스케줄 생성 `@Scheduled(cron = "0 0 18 * * *")`

로컬에서는 스케줄이 잘 작동하여 AWS EC2(Linux)에 배포

1분 단위로 실행 되는 `@Scheduled(cron = "0 * * * * *")` 스케줄은 잘 작동됨

아 이제 테스트 끝 ! 저녁 6시로 바꾸자 !

6시에 실행이 안됨 ..

계속 확인하다가 도저히 못찾겠어서 서비스는 그대로 두고 퇴근.

`새벽 3시에 실행됨 !!`

뭔가 시간의 문제일 것이다로 추측하여 구글링

<br>
<br>

## 원인

<br>

로컬 환경에서는 `Timezone(KST)`

배포 환경에서는 `Timezone(UTC)`

<br>
<br>

## 해결방법

<br>

`$ date` 로 현재 날짜 및 Timezone 확인

`$ sudo ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime` 로 KST로 수정

만약 위 작업을 하여도 되지 않는다면

<br> 

**한번 더 구글링**

<br>

```java
@Scheduled(cron = "0 0 18 * * *", zone = "Asia/Seoul")
```

위와 같이 Timezone을 직접 설정해주자.


> 리눅스 시간은 /etc/localtime 설정 파일의 내용에 따라서 시스템 시각이 바뀜

