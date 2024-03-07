---
layout: post
title: "API style (Options, Composition)"
subtitle: "API 종류"
category: "vue.js"
date: 2024-03-06
background: '/img/posts/codeImg.jpg'
---


## Options

`data` `methods` `mounted` 와 같은 객체를 사용하여 컴포넌트 로직을 정의

<br>

### 예제

```vue
<script>
export default {
  // data()에서 반환된 속성들은 반응적인 상태가 되어
  // `this`에 노출됩니다.
  data() {
    return {
      count: 0
    }
  },

  // methods는 속성 값을 변경하고 업데이트 할 수 있는 함수.
  // 템플릿 내에서 이벤트 헨들러로 바인딩 될 수 있음.
  methods: {
    increment() {
      this.count++
    }
  },

  // 생명주기 훅(Lifecycle hooks)은 컴포넌트 생명주기의
  // 여러 단계에서 호출됩니다.
  // 이 함수는 컴포넌트가 마운트 된 후 호출됩니다.
  mounted() {
    console.log(`숫자 세기의 초기값은 ${ this.count } 입니다.`)
  }
}
</script>

{% raw %}
<!-- /는 지워서 테스트 -->
<template>
  <button @click="increment">숫자 세기: {{ count }}</button>
</template>
{% endraw %}

```

<br>

> mounted() == DOM 생성 및 삽입

<br>
<br>
<br>

## Composition API

`Vue3에서 새로 추가된 함수 기반의 API` `컴포넌트 로직을 유연하게 구성 -> 코드의 재사용성과 가동성 향상`

**`script setup 사용`**

<br>

### 예제 (동일한 예제)

```vue
<script setup>
import { ref, onMounted } from 'vue'

// 반응적인 상태의 속성
const count = ref(0)

// 속성 값을 변경하고 업데이트 할 수 있는 함수.
function increment() {
  count.value++
}

// 생명 주기 훅
onMounted(() => {
  console.log(`숫자 세기의 초기값은 ${ count.value } 입니다.`)
})
</script>

<!-- /는 지워서 테스트 -->
{% raw %}
<template>
  <button @click="increment">숫자 세기: {{ count }}</button>
</template>
{% endraw %}
```

<br>

### 결론

**`Composition API + SFC (단일파일 컴포넌트)를 사용하자 !`**


<br>
<br>
<br>

<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://v3-docs.vuejs-korea.org/>
<div>
