---
layout: post
title: "computed vs watch"
subtitle: "기초 다지기"
category: "vue.js"
date: 2024-03-08
background: '/img/posts/codeImg.jpg'
---


## computed
`선언형 프로그래밍`

<br>

### 예제


`compute 사용 X` - 코드가 비대해지고 유지보수가 어렵다.

{% raw %}
```html
<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
```
{% endraw %}

<br>

`compute 사용 O`

```vue
{% raw %}
<div id="example">
  <p>원본 메시지: "{{ message }}"</p>
  <p>역순으로 표시한 메시지: "{{ reversedMessage }}"</p>
</div>
{% endraw %}
<script>
    var vm = new Vue({
    el: '#example',
    data: {
        message: '안녕하세요'
    },
    computed: {
        // 계산된 getter
        reversedMessage: function () {
        // `this` 는 vm 인스턴스를 가리킵니다.
        return this.message.split('').reverse().join('')
        }
    }
    })
</script>
```

<br>

**결과**

원본 메세지:"안녕하세요" <br>
역순으로 표시한 메세지:"요세하녕안"

<br>

**중요**

```vue
<script>
    console.log(vm.reversedMessage) // => '요세하녕안'
    vm.message = 'Goodbye'
    console.log(vm.reversedMessage) // => 'eybdooG'
</script>
```

`vm.reversedMessage`의 값은 항상 `vm.message`에 의존한다.

`vm.message`가 바뀔 때 `vm.reversedMessage`에 의존하는 바인딩을 모두 업데이트한다.

<br>

### computed 속성의 캐싱 vs 메소드

아래 예제와 같이 methods로 정의할수도 있음

```vue
<script>
    // 컴포넌트 내부
    methods: {
    reversedMessage: function () {
        return this.message.split('').reverse().join('')
    }
    }
</script>
```

`computed 속성은 종속 대상을 따라 저장(캐싱) 됨`

<br>

> computed 종속 대상이 변경되었을 때만 함수를 실행
> 
> methods 함수를 호출할 때마다 실행

<br>
<br>

## computed vs watch

`computed`의 값은 캐싱되기 때문에 리렌더링 되었을 때, 같은 값이 들어오면 연산 X<br>
템플릿 내의 값이 data와 종속되었을 경우 사용

`watch`는 같은 값이 들어와도 연산 O<br>
지정한 값이 변경된 시점에서 내가 원하는 액션(`api call`, `route.push()`)을 하기 원할 때 사용






<br>
<br>
<br>

<details open="open">
<summary>참고 링크</summary>
<div markdown="1">
<https://https://v2.ko.vuejs.org/v2/guide/computed.html/>
<div>
