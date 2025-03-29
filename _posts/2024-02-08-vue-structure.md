---
layout: post
title: "Vue 프로젝트 기본구조"
subtitle: "기초 다지기"
category: "vue.js"
date: 2024-02-08
background: '/img/posts/vue constructor main.png'
---

# 프로젝트 기본 구조

![aspect](/img/posts/vue_structure.png)

<br>

## index.html

`앱이 실행될 때 나타나는 html, 여기서 main.js를 불러옴`

```html
<body>
	<div id="app"></div>
	<script type="module" src="/src/main.js"></script>
</body>
```

<br>

## main.js

`가장 먼저 실행되는 javascript 파일`

```javascript
import { createApp } from 'vue'
import App from './App.vue'

import './assets/main.css'

createApp(App).mount('#app')
```

- 우리가 사용할 Vue 인스턴스를 생성
- 그 안에 router, store 등 라이브러리 설정

<br>

## App.vue

`최상위 컴포넌트`

```vue
<template>
  <Header />
  <Main />
  <Sidebar />
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import Sidebar from "./components/Sidebar.vue";

export default {
  components: { Header, Main, Sidebar },
};
</script>
```

- 컴포넌트를 활용하여 템플릿처럼 사용
- `RouterView` 컴포넌트 사용

<br> 
<br> 
<br>


<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://any-ting.tistory.com/39><br>
<https://blogcreator.blog/post/4>
<div>
