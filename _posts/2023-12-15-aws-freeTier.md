---
layout: post
title: "프리티어 서버(EC2) 멈춤"
subtitle: "문제 해결"
category: "blog"
date: 2023-12-15
background: '/img/posts/freetier ec2.png'
---

<br> 
<br> 
<br>

# 프리티어 서버(EC2) 멈춤

프리티어로 제공해주는 인스턴스 유형인 `t2.micro`은 RAM이 1GB밖에 되지 않는다.<br>
따라서 EC2가 도중 멈추는 현상이 발생

<br>
<br>

## 해결 방법

> Swap 메모리 (디스크 공간을 활용하여 만들어낸 가상 메모리) 추가

<br>
<br>

### 1. Swap 메모리 추가

```bash
$ sudo dd if=/dev/zero of=/swapfile bs=128M count=16 // 스왑파일 생성
$ sudo chmod 600 /swapfile // 권한 부여
```
<br>

### 2. Swap 메모리를 Swap 파일로 대체

```bash
$ sudo mkswap /swapfile // Swap 메모리를 Swap 파일로 포맷
```
<br>

### 3. Swap 메모리 활성화

```bash
$ sudo swapon /swapfile // Swap 메모리 활성화
$ sudo swapon -s    // SWap 파일의 정보 및 크기 출력
```
<br>

### 4. Swap 메모리 시스템이 시작되더라도 자동 활성화
```bash
$ sudo vi /etc/fstab 

# 마지막 행에 추가하기
/swapfile swap swap defaults 0 0
```
<br>

### 5. 현재의 메모리 사용 및 가용 메모리에 대한 정보 확인
```bash
$ sudo free -h 
```

<br>

### 기타 정보
```bash
# Swap 메모리 삭제
sudo rm -r swapfile

# 단일 Swap 메모리 비활성화
$ sudo swapoff swapfile

# 모든 Swap 메모리 비활성화
$ sudo swapoff -a
```


<br> 
<br> 
<br>

**참고 URL : <https://velog.io/@hwsa1004/AWS-EC2-EC2-%EB%A9%88%EC%B6%A4%EB%8B%A4%EC%9A%B4CPU-%EC%82%AC%EC%9A%A9%EB%A5%A0-100-%ED%95%B4%EA%B2%B0%ED%95%98%EA%B8%B0>**
