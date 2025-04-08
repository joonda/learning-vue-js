## 노트

### 1. Vue Component 소개
* `Vue Component`
* `Component 분리 개발`

### 2. Vue Component 등록과 표시

`vue3` > `component.html`
```html
<body>
  <div id="app">
    <app-header></app-header>
  </div>
</body>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  Vue.createApp({
    components: {
      'app-header': {
        template: '<h1>Components Register</h1>'
      }
    }
  }).mount('#app');
</script>
```
* `components` 옵션을 통해서 `component`를 지정할 수 있다.

### 3. Vue Component 통신 방식
* 상위 컴포넌트에서 아래로 데이터가 흐르고 (prop), 아래에서 위로는 이벤트가 올라가는 구조를 갖게 된다.

### 4. Vue Component Props
* `vue3` > `props.html`
```html
<body>
  <div id="app">
    <app-header v-bind:title="appTitle"></app-header>
  </div>
</body>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  Vue.createApp({
    data() {
      return {
        appTitle: 'props delivery'
      }
    },
    components: {
      'app-header': {
        template: '<h1>{{title}}</h1>',
        props: ['title']
      }
    }
  }).mount('#app');
</script>
```

* `v-bind` 옵션을 통해서 props를 넘길 수 있다.
* `data` 안에 있는 `appTitle` 값을 넘기도록 진행, `{{title}}`로 `component`에 전달한다.

### 5. Event Emit 소개
* 하위 컴포넌트에서 상위 컴포넌트로 통신할 수 있는 방법
* 이벤트 발생 예시
```javascript
this.$emit('event');
```

```html
<div id="app">
  <child-component v-on:이벤트 명="상위 컴포넌트의 실행할 메서드 명 또는 연산"><child-component>
</div>
```

### 6. Event Emit 구현
```html
<body>
  <div id="app">
    <app-contents v-on:refresh="showAlert"></app-contents>
  </div>
</body>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  
  var appContents = {
    template: `
      <p>
        <button v-on:click="sendEvent">갱신</button>
      </p>
    `, 
    methods: {
      sendEvent() {
        this.$emit('refresh');
      }
    }
  }

  Vue.createApp({
    methods: {
      showAlert() {
        alert('새로고침');
      }
    },
    components: {
      'app-contents' : appContents
    }
  }).mount('#app');
</script>
```
* refresh 이벤트가 발생했을 때, showAlert() 함수를 실행하는 것!
* 이벤트 발생 -> `this.$emit('refresh')`
* 이벤트 감지 -> `<app-contents v-on:refresh="showAlert"></app-contents>`
* 처리 함수 -> `methods : { showAlert() {...} }`

### 7. 같은 레벨의 컴포넌트간 데이터 전달 방법

```html
<body>
  <div id="app">
    <app-header v-bind:app-title="message"></app-header>
    <app-contents v-on:login="receive"></app-contents>
  </div>
</body>
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  var appHeader = {
    props: ['appTitle'],
    template: '<h1>{{appTitle}}</h1>'
  };

  var appContents = {
    template: `
      <p>
        <button v-on:click="sendEvent">로그인</button>
      </p>
    `,
    methods: {
      sendEvent() {
        this.$emit('login');
      }
    }
  };

  Vue.createApp({
    data() {
      return {
        message: ''
      }
    },
    methods: {
      receive() {
        console.log('받음');
        this.message = '로그인 됨'
      }
    },
    components: {
      'app-header': appHeader,
      'app-contents': appContents
    }
  }).mount('#app')
</script>
```
* 같은 레벨의 컴포넌트 간 데이터 전달 방법
* 하위 컴포넌트에서 루트로 이벤트를 올려 보내고, 그 다음에 루트에서 바뀐 이벤트에 prop을 전달하는 방법으로 전달한다.