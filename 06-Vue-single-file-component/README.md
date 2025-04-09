## 노트

### 1. Vue Single File Component 소개
* 화면의 특정 영역에 대한 `HTML`, `CSS`, `JS` 코드를 한 파일에서 관리하는 방법
```html
<!-- .vue 파일 구조 -->
<template>
  <!-- html (뷰 컴포넌트의 표현단, 템플릿 문법) -->
</template>

<script>
  // 자바스크립트 (뷰 컴포넌트 내용)
</script>

<style>
  /* CSS (뷰 템플릿의 스타일링) */
</style>
```
* 브라우저에서는 `.vue` 파일이 인식될 수가 없기 때문에 별도의 변환과정을 거친다.

### 2. App Component
* 컴포넌트 명명 규칙
    * 싱글 파일 컴포넌트 레벨에서는 `파스칼 케이스`로 작성하는 것을 추천
        * e.g. `HelloWorld`
    * 일관된 한가지 방식으로만 준수하는 것을 추천함 (`카멜 케이스` or `하이픈` 등)

### 3. 싱글 파일 컴포넌트 코드 작성 팁
* vbc + `tab`
    * 아래 코드 처럼 자동완성 기능
```vue
<template>
  <div>

  </div>
</template>

<script>
  export default {
    
  }
</script>

<style scoped>

</style>
```
* vda + `tab`
```vue
data() {
    return {
        key: value
        }
}
```

`src` > `App.vue`
```vue
<template>
  <div>
    {{ message }}
  </div>
  <button @click="showAlert">Warning</button>
</template>

<script>
  export default {
    data() {
      return {
        message: 'hi'
      }
    },
    methods: {
      showAlert() {
        alert('hello')
      }
    }
  }
</script>

<style scoped>

</style>
```
* `v-on:click` -> `@click` 으로 축약할 수 있다.

### 4. Vue 컴포넌트 등록 방법 및 명명 규칙

* `src` > `components` > `AppHeader.vue`
```vue
<template>
    <h1>App Header</h1>
</template>

<script>
    export default {
        
    }
</script>

<style scoped>

</style>
```
* AppHeader Component를 만든다.

* `src` > `App.vue`
```vue
<template>
  <AppHeader></AppHeader>
  <div>
    {{ message }}
  </div>
  <button @click="showAlert">Warning</button>
</template>

<script>
import AppHeader from './components/AppHeader.vue';

  export default {
    components: {
      'AppHeader': AppHeader
    },

    data() {
      return {
        message: 'hi'
      }
    },
    methods: {
      showAlert() {
        alert('hello')
      }
    }
  }
</script>

<style scoped>

</style>
```
* `App.vue` 파일에 `script`부분에 import 진행
* `component` 에 등록, 
  * `component`의 `'AppHeader' : AppHeader` 부분을 그냥 AppHeader로 통일 해도 상관 없다.
```vue
export default {
  components: {
    AppHeader
  },
}
```

### 5. 싱글파일 컴포넌트의 props, event emit
#### props
* `src` > `App.vue`
```vue
<template>
  <AppHeader :app-title="message"></AppHeader>
  <div>
    {{ message }}
  </div>
  <button @click="showAlert">Warning</button>
</template>

<script>
import AppHeader from './components/AppHeader.vue';

  export default {
    components: {
      AppHeader
    },

    data() {
      return {
        message: '앱 헤더 컴포넌트'
      }
    },
    methods: {
      showAlert() {
        alert('hello')
      }
    }
  }
</script>

<style scoped>

</style>
```
* `data`의 `message`를 prop으로 넘겨준다 (`:app-title="message"`)

`src` > `components` > `AppHeader.vue` 
```vue
<template>
    <h1>{{ appTitle }}</h1>
</template>

<script>
    export default {
        props: ['appTitle']
    }
</script>

<style scoped>

</style>
```
* props로 받을 이름을 지정 (`props: ['appTitle']`)
* `{{ appTitle }}` 로 prop을 받는다.

#### event emit
`src` > `components` > `AppHeader.vue` 
```vue
<template>
    <h1>{{ appTitle }}</h1>
    <button @click="changeTitle">button</button>
</template>

<script>
    export default {
        props: ['appTitle'],
        methods: {
            changeTitle() {
                this.$emit('change')
            }
        }
    }
</script>

<style scoped>

</style>
```
* `@click`으로 `"changeTitle"` 메서드를 지정, `$emit`으로 상위 컴포넌트에 `change` 라는 이벤트를 보낸다

* `src` > `App.vue`
```vue
<template>
  <AppHeader 
    :app-title="message"
    v-on:change="changeMessage">
  </AppHeader>
</template>

<script>
import AppHeader from './components/AppHeader.vue';

  export default {
    components: {
      AppHeader
    },

    data() {
      return {
        message: '앱 헤더 컴포넌트'
      }
    },
    methods: {
      changeMessage() {
        this.message = '변경됨'
      }
    }
  }
</script>

<style scoped>

</style>
```
* `v-on:change`로 이벤트를 받고, 하위에서 발생한 이벤트를 감지해서 `changeMessage` 메서드를 실행
* 이로서 하위 컴포넌트에서 이벤트가 발생하면, 상위 컴포넌트가 해당 이벤트를 받아 후속 동작을 처리