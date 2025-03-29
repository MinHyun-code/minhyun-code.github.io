---
layout: post
title: "&lt;script setup&gt"
subtitle: "문법"
category: "vue.js"
date: 2024-03-07
background: '/img/posts/script setup.png'
---


## &lt;script setup&gt;

`SFC(싱글 파일 컴포넌트)` `컴포지션 API` 환경에서 더 쉽게 읽거나 사용하기 위한 컴파일 문법

<br>

### 장점

1. 적은 상용구로 간결한 코드
2. 순수 Typescript를 사용하여 props 및 emit 이벤트를 선언하는 기능
3. 개선된 런타임 성능 (템플릿은 중간 프록시 없이 동일한 범위의 렌더 함수로 컴파일 됨)
4. 개선된 IDE 타입 추론 성능 (언어 서버가 코드에서 타입을 추출하는 작업 감소)

<br>

### 사용방법

`script 선언 시 setup 작성`

```vue
<script setup>
  console.log('안녕, script setup!');
</script>
```

> 
> 컴포넌트를 처음 가져올 때 한 번만 실행하는 `<script>`와 달리, 
> `<script setup>` 내부의 코드는 컴포넌트 인스턴스가 생성될 때마다 실행
> 

<br>
<br>

## &lt;script setup&gt; 과 setup()의 차이

**`props 선언하는 부분` `return 부분`**

### setup() 예제

```vue
<!-- MyBook.vue -->
<template>
  {% raw %}
  <div>{{ collectionName }}: {{ readersNumber }} {{ book.title }}</div>
  <button @click="incresement">incresement</button>
  {% endraw %}
</template>

<script>
import { ref, reactive } from "vue";

export default {
  props: {
    collectionName: String,
  },
  setup(props) {
    const readersNumber = ref(0);
    const book = reactive({ title: "Vue 3 Guide" });
    const incresement = () => {
      readersNumber.value += 1;
    };
    // expose to template
    return {
      readersNumber,
      book,
      incresement,
    };
  },
};
</script>
```

<br>

### &lt;script setup&gt; 예제

```vue
<!-- MyBook.vue -->
<template>
  {% raw %}
  <div>{{ collectionName }}: {{ readersNumber }} {{ book.title }}</div>
  <button @click="incresement">incresement</button>
  {% endraw %}
</template>

<script setup>
  import { ref, reactive } from "vue";
  const props = defineProps({
    collectionName: String,
  });

  const readersNumber = ref(0);
  const book = reactive({ title: "Vue 3 Guide" });
  const incresement = () => {
    readersNumber.value += 1;
  };
</script>
```


<br>
<br>
<br>

<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://v3-docs.vuejs-korea.org/>

<https://mine-it-record.tistory.com/640#google_vignette/>
<div>
