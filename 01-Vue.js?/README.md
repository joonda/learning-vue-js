## 노트

### 1. Vue.js란 ?
* 간단한 화면 UI 개발부터 라우팅, SSR 등의 애플리케이션 레벨의 개발을 지원하는 프레임워크
* 라우팅 -> 페이지 간의 이동
* SSR -> 서버 사이드 렌더링
    * Nuxt -> Vue.js로 SSR을 구현할 때 사용하는 기술
* React에 비해 진입 장벽이 낮고 쉽게 배울 수 있다.
* 개발 생산성 높음, 자바스크립트 지식이 크게 요구되지 않는다.

### 2. Vue 2 vs. Vue 3
* Vue 3 -> 라이브러리 내부 로직 재작성
* 주요 개발 도구들 변경
    * e.g. 뷰 개발자 도구, VSCode 플러그인, Vite 기반 프로젝트 생성
* Composition API, Teleport 등 새로운 문법 지원
* 리액티비티 시스템 기반 API 변경
* 공식 문서 변경

### 3. Vue 3 코드 작성 방법
* Vue 시작은 Option Api를 먼저 쓰는 것을 추천

```javascript
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app">{{ message }}</div>

<script>
  const { createApp } = Vue

  createApp({
    data() {
      return {
        message: 'Hello Vue!'
      }
    }
  }).mount('#app')
</script>
```

### 4. 개발 환경 구성
* VSCode, Node.js
* VSCode plugin
    * Vue vscode snippets
    * live server
    * Material Icon Theme
    * Night Owl
    * Vetur (Vue 2)
    * Volar (Vue 3)

### 5. Vue.js 개발자 도구 안내

* [Vue.js 개발자 도구](https://chromewebstore.google.com/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd)

### 6. 강의 교안과 소스 코드 안내
* [Vue 교안 참고](https://joshua1988.github.io/vue-camp/)

### 7. Hello World(Vue.js 인스턴스)

`index.html`

```javascript
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app">
    {{ message }}
</div>

<script>
    Vue.createApp({
        data() {
            return {
                message: 'hi'
            }
        }
    }).mount('#app');
</script>
```