## 노트

### 1. 프로젝트 생성 및 로그인 폼 UI 구성
`src` > `App.vue`
```vue
<template>
  <form action="" >
    <div>
      <label for="userId">ID : </label>
      <input id="userId" type="text" v-model="username">
    </div>
    <div>
      <label for="password">PW : </label>
      <input type="text" v-model="password">
    </div>
    <button type="submit">Login</button>
  </form>
</template>

<script>
  export default {
    data() {
      return {
        username: '',
        password: '',
      }
    },
  }
</script>

<style scoped>

</style>
```
* `v-model`로 양방향 바인딩을 진행
* data의 값과 화면의 입력 값이 자동으로 동기화 된다.

### 2. 홈 이벤트 제어 및 서버로 데이터 전송
`src` > `App.vue`

```vue
<template>
  <form action="" @submit.prevent="submitForm">
    <div>
      <label for="userId">ID : </label>
      <input id="userId" type="text" v-model="username">
    </div>
    <div>
      <label for="password">PW : </label>
      <input type="text" v-model="password">
    </div>
    <button type="submit">Login</button>
  </form>
</template>

<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        username: '',
        password: '',
      }
    },
    methods: {
      submitForm() {
        const data = {
          username: this.username,
          password: this.password
        }
        axios.post('https://jsonplaceholder.typicode.com/users/', data)
        .then(response => {
          console.log(response)
        });
      }
    }
  }
</script>

<style scoped>

</style>
```
* `v-model`로 실시간으로 데이터와 바인딩
* `submitForm`을 정의, this를 활용하여 현재의 username, password를 받아온다.
* `@submit`에서 `submitForm()`을 지정,
  * `@submit.prevent`를 활용하여 폼 제출 시 자동 새로고침을 방지하고, submitForm 메서드를 실행한다.
* `submitForm` 메서드 내부에서는 `this.username`, `this.password`를 통해 입력된 값을 가져오고, axios를 사용해 서버로 `POST` 요청을 보낸다

### 3. Vue Composition API 코드로 변환하기

```vue
<template>
  <form action="" @submit.prevent="submitForm">
    <div>
      <label for="userId">ID : </label>
      <input id="userId" type="text" v-model="username">
    </div>
    <div>
      <label for="password">PW : </label>
      <input id="password" type="text" v-model="password">
    </div>
    <button type="submit">Login</button>
  </form>
</template>

<script>
  import axios from 'axios';
  import {ref} from 'vue'

  export default {
    setup() {
      // data
      const username = ref('');
      const password = ref('');

      // methods
      const submitForm = () => {
        axios.post('https://jsonplaceholder.typicode.com/users/', {
          username: username.value,
          password: password.value
        }).then(response => {
          console.log(response)
        })
      }

      return { username, password, submitForm }
    },
  }
</script>

<style scoped>

</style>
```
* setup으로 간단하게 축약할 수 있다.