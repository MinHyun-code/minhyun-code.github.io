---
layout: post
title: "Skeleton Screen"
subtitle: "UI"
category: "vue.js"
date: 2024-02-27
background: '/img/posts/skeleton main.png'
---

> 데이터를 보여주면서 화면이 조금씩 밀리는 현상이 생겨
> 깔끔하지가 않아 공부하게 됨

# Skeleton Screen

`페이지 콘텐츠가 완전히 로딩되기 전에 나타나는 시각적 자리 표시자`

<br>


### 구현 방법

**Skeleton.vue**

```vue
<script setup>
import { ref } from 'vue'
import $ from 'jquery';

defineProps({
  msg: String,
})

const hideskeleton = () => {
    const skeletonItem = document.querySelectorAll('.skeleton_loading');
    skeletonItem.forEach(element => {
    $(element).fadeOut();
    });
};
// 테스트 코드 
window.onload = setTimeout(hideskeleton, 1000);
// 실제 코드 
// window.onload = hideskeleton;
</script>

<template>
  <article>
    <div class="flex">
      <div class="item">
        <div class="item-img">
          <div class="skeleton_loading">
            <div class="skeleton_img"></div>
          </div>
          <img class="img" src="https://image.utoimage.com/preview/cp872722/2022/12/202212008462_500.jpg" />
        </div>
      </div>
      <div class="item">
        <div class="item-img">
          <div class="skeleton_loading">
            <div class="skeleton_img"></div>
          </div>
          <img class="img" src="https://image.utoimage.com/preview/cp872722/2022/12/202212008462_500.jpg" />
        </div>
      </div>
      <div class="item">
        <div class="item-img">
          <div class="skeleton_loading">
            <div class="skeleton_img"></div>
          </div>
          <img class="img" src="https://image.utoimage.com/preview/cp872722/2022/12/202212008462_500.jpg" />
        </div>
      </div>
      <div class="item">
        <div class="item-img">
          <div class="skeleton_loading">
            <div class="skeleton_img"></div>
          </div>
          <img class="img" src="https://image.utoimage.com/preview/cp872722/2022/12/202212008462_500.jpg" />
        </div>
      </div>
      <div class="item">
        <div class="item-img">
          <div class="skeleton_loading">
            <div class="skeleton_img"></div>
          </div>
          <img class="img" src="https://image.utoimage.com/preview/cp872722/2022/12/202212008462_500.jpg" />
        </div>
      </div>
      <div class="item">
        <div class="item-img">
          <div class="skeleton_loading">
            <div class="skeleton_img"></div>
          </div>
          <img class="img" src="https://image.utoimage.com/preview/cp872722/2022/12/202212008462_500.jpg" />
        </div>
      </div>
      <div class="item">
        <div class="item-img">
          <div class="skeleton_loading">
            <div class="skeleton_img"></div>
          </div>
          <img class="img" src="https://image.utoimage.com/preview/cp872722/2022/12/202212008462_500.jpg" />
        </div>
      </div>
      <div class="item">
        <div class="item-img">
          <div class="skeleton_loading">
            <div class="skeleton_img"></div>
          </div>
          <img class="img" src="https://image.utoimage.com/preview/cp872722/2022/12/202212008462_500.jpg" />
        </div>
      </div>
      <div class="item">
        <div class="item-img">
          <div class="skeleton_loading">
            <div class="skeleton_img"></div>
          </div>
          <img class="img" src="https://image.utoimage.com/preview/cp872722/2022/12/202212008462_500.jpg" />
        </div>
      </div>
      
    </div>
  </article>
</template>
```

<br>
<br>

**style.css**


```style
:root {
  --bg-color: #f4f4f4;
}
html,
body {
  margin: 0;
}
body {
  background: var(--bg-color);
}
article {
  max-width: 1000px;
  margin: 1rem auto 0;
}
img {
  border-radius: 1rem;
}

/*========스켈레톤 애니메이션 시작========*/
h1 {
 text-align: center;
 margin-top: 2rem;
 margin-bottom: 0;
}
.flex {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  justify-content: space-around;
  width: 100%;
  text-align: justify;
}
@media (max-width: 767.98px) {
  .flex {
      display: grid;
  }
}
.item {
  padding: 1rem;
}
.item-img {
  position: relative;
  width: 16rem;
  height: 25rem;
}

/*스켈레톤 메인 컨테이너*/
.skeleton_loading {
  position: absolute;
  width: 100%;
  height: 100%;
  background: var(--bg-color);
}
/* 스켈레톤 이미지 */
.skeleton_img {
  width: 100%;
  height: 100%;
}

/* 스켈레톤 텍스트 */
.skeleton_text {
  margin-bottom: 0.5rem;
  height: 1rem;
}
.skeleton_text:nth-child(1) {
  width: 50%;
  height: 1.5rem;
}
.skeleton_text:nth-child(2) {
  width: 20%;
  height: 0.8rem;
}
.skeleton_text:last-child {
  width: 80%;
}

.skeleton_loading * {
  background: linear-gradient(120deg, #e5e5e5 30%, #f0f0f0 38%, #f0f0f0 40%, #e5e5e5 48%);
  border-radius: 1rem;
  background-size: 200% 100%;
  background-position: 100% 0;
  animation: load 1s infinite;
}

@keyframes load {
  100% {
      background-position: -100% 0;
  }
}

/* 실제 콘텐츠 이미지 */
.img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.item-text {
  position: relative;
  width: 320px;
}
/* 실제 콘텐츠 */
h3 {
  margin-bottom: 0.5rem;
  margin-top: 0.8rem;
}
.create-date {
  font-size: smaller;
  margin-bottom: 0.5rem;
}
.description {
  font-size: 0.9rem;
  color: #5f5f5f;
  word-break: break-all;
  overflow: hidden;
  -webkit-line-clamp: 2;
  word-break: break-all;
  white-space: normal;
  text-overflow: ellipsis;
  -webkit-box-orient: vertical;
  display: -webkit-box;
}

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
}

@media (prefers-color-scheme: light) {
  :root {
    color: #213547;
    background-color: #ffffff;
  }
  a:hover {
    color: #747bff;
  }
  button {
    background-color: #f9f9f9;
  }
}

```

<br>
<br>

### 결과

![alt text](/img/posts/skeleton.png)

<br>
<br>

![alt text](/img/posts/skeleton2.png)

<br> 
<br> 
<br>
