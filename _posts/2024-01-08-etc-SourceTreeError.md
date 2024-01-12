---
layout: post
title: "SourceTree private repository 못 가져오는 현상"
subtitle: "문제 해결"
category: "etc"
date: 2024-01-08
background: '/img/posts/codeImg.jpg'
---

<br>

## 현상

1. 운영 고객사 추가로 인해 organization 접근 후 repository clone

2. 자꾸 repository가 없다는 에러 발생

<br>

> 에러 내용
> 
> remote: Repository not found. <br>
> fatal: repository 'https://github.com/받으려는레포지토리.git/' not found

<br> 
<br>

## 해결과정

1. SourceTree 내에서 회사 계정과 개인 계정 2개가 등록되어 있어 계정이 꼬일 가능성 충분 <br>
   -> 개인 계정 삭제 `해결 X`

2. Window 자격증명에서 SourceTree와 Git과 관련된 증명 전부 삭제 -> `해결 X`

3. 구글링 결과 SourceTree에서 OAuth가 정상적으로 작동하지 않을수도 있다는 내용을 확인 <br>
   -> Personal Access Token 사용하여 계정 접근 `해결 O`

<br>
<br>
<br> 