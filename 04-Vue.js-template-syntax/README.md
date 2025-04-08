## 노트

### 1. Vue 템플릿 문법(Template Syntax) 소개
* 데이터 바인딩과 디렉티브로 나뉜다.
#### 데이터 바인딩
```html
<div>{{message}}</div>
```

#### 디렉티브
* `v-if`, `v-bind`, `v-on`, `v-for`, ...
```html
<div>
  Hello <span v-if="show">Vue.js</span>
</div>
<script>
  new Vue({
    data: {
      show: false
    }
  })
</script>
```

### 2. Vue 디렉티브: v-if, v-show

`vue3` > `data-binding.html`
```html
<body>
  <div id="app">
    <p v-if="login">로그인 되었습니다.</p>
    <p v-else>로그인 하세요.</p>
    <button v-on:click="loginUser">로그인</button>

    <hr>

    <p v-show="login">로그인 되었습니다.</p>
    <button v-on:click="loginUser">로그인</button>
  </div>
</body>
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  Vue.createApp({
    data() {
      return {
        login: false
      }
    },
    methods: {
      loginUser() {
        this.login = !this.login;
      }
    }
  }).mount('#app')
</script>
```

### Vue 데이터 바인딩: id, class, style
* 각각 HTML의 Attribute에 동적으로 연결하는 것 -> 데이터 바인딩

```html
<style>
.primary {
  color: coral;
}
</style>

<body>
  <div id="app">
    <h1>클래스 바인딩</h1>
    <!-- v-bind:class -> :class로 축약 가능 -->
    <div :class="textClass">데이터 바인딩 예제</div>
    <h1>아이디 바인딩</h1>
    <section :id="sectionId" :style="sectionStyle">
      반갑습니다.
    </section>
  </div>
</body>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  Vue.createApp({
    data() {
      return{
        textClass: 'primary',
        sectionId: 'tab1',
        sectionStyle: {color: 'red'}
      }
    }
  }).mount('#app')
</script>
```
* `v-bind`는 `:`으로 축약이 가능하다 (실무에서는 주로 `:`을 사용한다)
* 동적으로 id, class, style 등의 변경을 용이하게 해줄 수 있다