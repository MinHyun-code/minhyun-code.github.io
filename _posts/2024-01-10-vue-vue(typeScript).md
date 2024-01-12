---
layout: post
title: "Vue3 ref, reactive"
subtitle: "기초 다지기"
category: "vue.js"
date: 2024-01-10
background: '/img/posts/codeImg.jpg'
---

**`Vue2 data() 와 ref()`**

```vue
 <div id="app">
    <template>
      {{text}}
    </template>
  </div>

  <script>
    data() {
      return {
        text: "Hello"
      }
    },
    mounted() {
      setTimeout(()=> {
        this.text = this.text + " Vue2"
      },2000)
    }
  </script>
```
<br>
<br>


**`Vue3 data() 와 ref()`**

```vue
<div id="app">
  {{text1}}<br>
  {{text2}}<br>
</div>

<script>
  const {  
    ref
  } = Vue;

  const App = {
    setup() {
      let text1 = "Hello";
      let text2 = ref("Hello");

      setTimeout(() => {
        text1 = text1 + " Vue3"; 
        text2.value = text1 + " Jo!!"; //ref 는 .value로 접근해야된다
      }, 2000);

      return { 
        text1, 
        text2,
      };
    },
  };
</script>
```



<br>



<br> 
<br> 
<br>
