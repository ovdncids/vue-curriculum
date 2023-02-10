# Vue.js
[데모](https://curriculums-min.web.app)

## Node.js
https://nodejs.org

## NVM (Node Version Manager)
https://github.com/ovdncids/react-curriculum/blob/master/NVM.md

## Vue CLI
https://kr.vuejs.org/v2/guide/index.html

https://cli.vuejs.org/guide/installation.html
```sh
# Vue CLI 설치
npm install -g @vue/cli

# Vue.js 프로젝트 생성
vue create vue-study
## Normal type without Test ([Vue 2] dart-sass, babel, router, vuex, eslint) 선택

cd vue-study
code .

# VSCode로 해당 디렉토리 열기
## build
npm run build
npm install -g serve
serve -s dist

## 프로젝트 실행
npm run serve
```

## GIT
소스 관리를 위해 사용한다. 어느 파일이 언제 어떻게 변경 되었는지 쉽게 볼 수 있다.

**GIT 설치**

**VSCode 확장 Git Graph 설치**

## 필요 없는 파일 지우기
```diff
- src/assets/logo.png
- src/views (폴더 삭제)
- src/components/HelloWorld.vue
```

src/main.js (router 부분 주석 처리)
```js
// import router from './router'
new Vue({
  // router,
```

## Markup
src/App.vue (덮어 씌우기)
```html
<template>
  <div id="app">
    <header>
      <h1>Vue.js study</h1>
    </header>
    <hr />
    <div class="container">
      <nav class="nav">
        <ul>
          <li><h2>Users</h2></li>
          <li><h2>Search</h2></li>
        </ul>
      </nav>
      <hr />
      <section class="contents">
        <div>
          <h3>Users</h3>
          <p>Contents</p>
        </div>
      </section>
      <hr />
    </div>
    <footer>Copyright</footer>
  </div>
</template>
```

src/assets/scss/App.scss
```scss
* {
  margin: 0;
  font-family: -apple-system,BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}
a:link, a:visited {
  text-decoration: none;
  color: black;
}
a.active {
  color: white;
}
h1, footer, .nav ul {
  padding: 0.5rem;
}
h4, li {
  margin: 0.5rem 0;
}
hr {
  display: none;
  margin: 1rem 0;
  border: 0;
  border-top: 1px solid #ccc;
}
input[type=text] {
  width: 120px;
}

.d-block {
  display: block;
}
.container {
  display: flex;
  border-top: 1px solid #ccc;
  border-bottom: 1px solid #ccc;
}
.nav {
  min-height: 300px;
  background-color: #4285F4;
}
.nav ul {
  list-style: none;
}
.contents {
  flex: 1;
  padding: 1rem;
}

.table-search {
  border: 1px solid rgb(118, 118, 118);
  border-collapse: collapse;
  text-align: center;
}
.table-search th, .table-search td {
  padding: 0.2rem;
}
.table-search td {
  border-top: 1px solid rgb(118, 118, 118);
  min-width: 100px;
}
```

src/main.js (App.scss 부르기)
```js
import '@/assets/scss/App.scss'
```

## Vue Component 만들기
HeaderComponent.vue, NavComponent.vue, FooterComponent.vue 이렇게 Component 별로 파일을 나눈다.

src/App.vue
```html
<!-- 가장 아래에 추가 -->
<script>
import HeaderComponent from './components/HeaderComponent.vue'
import NavComponent from './components/NavComponent.vue'
import FooterComponent from './components/FooterComponent.vue'

export default {
  components: {
    HeaderComponent,
    NavComponent,
    FooterComponent
  }
}
</script>
```

src/components/HeaderComponent.vue
```html
<template>
  <header>
    <h1>Vue.js study</h1>
  </header>
</template>
```

src/App.vue
```diff
- <header>
-  <h1>Vue.js study</h1>
- </header>
+ <HeaderComponent></HeaderComponent>

- <nav class="nav">
-   <ul>
-     <li><h2>Users</h2></li>
-     <li><h2>Search</h2></li>
-   </ul>
- </nav>
+ <NavComponent></NavComponent>

- <footer>Copyright</footer>
+ <FooterComponent></FooterComponent>
```

### v-show, v-if, props
src/App.vue
```html
<HeaderComponent v-show="false"></HeaderComponent>

<NavComponent v-if="false"></NavComponent>

<FooterComponent :title="'카피라이트'"></FooterComponent>
```

src/components/FooterComponent.vue
```diff
- <FooterComponent>Copyright</FooterComponent>
+ <FooterComponent>{{title}}</FooterComponent>
```
```js
<!-- 가장 아래에 추가 -->
<script>
export default {
  props: {
    title: {
      default: 'Copyright'
    }
  }
}
</script>
```
**props는 부모 Component에서 자식 Component로 값을 전달 한다**

<!--
### emit (자식 Component에서 부모 Component의 함수 호출)
src/App.vue
```js
<Footer @callParentMethod="parentMethod"></Footer>

<script>
export default {
  methods: {
    parentMethod(parameter1) {
      console.log(parameter1, this)
    }
  }
}
</script>
```

src/components/FooterComponent.vue
```js
<footer @click="$emit('callParentMethod', 'argument1')">{{title}}</footer>
```
-->

## Vue Router
src/App.vue (div 태그를 router-view 태그로 변경)
```diff
<template>
  <section class="contents">
-   <div>
-     <h3>Users</h3>
-     <p>Contents</p>
-   </div>
+   <router-view></router-view>
```

src/components/contents/UsersComponent.vue
```html
<template>
  <div>
    <h3>Users</h3>
    <p>Contents</p>
  </div>
</template>
```

src/components/contents/SearchComponent.vue (동일)

src/router/index.js
```diff
- import Home from '../views/Home.vue'
```
```js
import Users from '../components/contents/UsersComponent.vue'
import Search from '../components/contents/SearchComponent.vue'
```

```diff
- const routes = [
- ...
- ]
```
```js
const routes = [
  { path: '/', redirect: '/users' },
  {
    path: '/users',
    name: 'Users',
    component: Users
  },
  {
    path: '/search',
    name: 'Search',
    component: Search
  }
]
```

src/main.js (router 부분 주석 풀기)
```js
import router from './router'
new Vue({
  router,
```

**주소 창에서 router 바꾸어 보기**

src/components/NavComponent.vue (li 태그 부분 덮어 씌우기)
```html
<li><h2><router-link :to="{name: 'Users'}" active-class="active">Users</router-link></h2></li>
<li><h2><router-link :to="{path: '/search'}" active-class="active">Search</router-link></h2></li>
```

**여기 까지가 Markup 개발자 분들이 할일 입니다.**

## Users Store 만들기
**Store 개념 설명**

Component가 사용하는 글로벌 함수 또는 변수라고 생각하면 쉽다, state 값이 변하면 해당 값을 바라 보는 모든 Component가 수정 된다.

**Store 사용 하는 이유**

Component에 변경된 사항을 다시 그리기 위해서 Store를 사용 한다.

src/store/usersModule.js
```js
export const usersModule = {
  state: {
    users: [],
    user: {
      name: '',
      age: ''
    }
  },
  mutations: {
  },
  actions: {
  }
}
```

**usersModule.js를 Store에 등록**

src/store/index.js
```diff
+ import { usersModule } from './usersModule.js'

export default new Vuex.Store({
  modules: {
+   $users: usersModule
  }
```

### Users Component Vuex Store 주입
src/components/contents/UsersComponent.vue
```js
<template>
  <div>
    <h3>Users</h3>
    <hr class="d-block" />
    <div>
      <h4>Read</h4>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Age</th>
            <th>Modify</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>홍길동</td>
            <td>20</td>
            <td>
              <button>Update</button>
              <button>Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <hr class="d-block" />
    <div>
      <h4>Create</h4>
      <input type="text" placeholder="Name" />
      <input type="text" placeholder="Age" />
      <button>Create</button>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    user() {
      return this.$store.state.$users.user
    }
  },
  methods: {
  },
  created() {
    console.log(this.user)
    this.user.name = ''
    this.user.age = ''
  }
}
</script>
```

**computed, methods 차이 설명**

**debugger 설명**
```js
debugger
```
**Unexpected 'debugger' statement 발생할 경우**

package.json
```diff
"eslintConfig": {
  "rules": {
+   "no-debugger": 1
  }
}
// 0 = off, 1 = warn, 2 = error
```
**또는**
```js
debugger // eslint-disable-line no-debugger
```

## Users Store CRUD
### Create
src/store/usersModule.js
```js
  actions: {
    usersCreate(thisStore, user) {
      thisStore.state.users.push({
        name: user.name,
        age: user.age
      })
      console.log('Done usersCreate', thisStore.state.users)
    }
  }
```

src/components/contents/UsersComponent.vue
```html
<input type="text" placeholder="Name" v-model="user.name" />
<input type="text" placeholder="Age" v-model="user.age" />
<button @click="usersCreate(user)">Create</button>
```
```js
  methods: {
    usersCreate(user) {
      this.$store.dispatch('usersCreate', user)
    }
  }
```

### Read
src/store/usersModule.js
```js
  mutations: {
    usersRead(state, users) {
      state.users = users
    }
  },
  actions: {
    usersRead(thisStore) {
      const users = [{
        name: '홍길동',
        age: 20
      }, {
        name: '춘향이',
        age: 16
      }]
      thisStore.commit('usersRead', users)
      console.log('Done usersRead', thisStore.state.users)
    }
  }
```

src/components/contents/UsersComponent.vue (16줄)
```diff
- <tr>
-  <td>홍길동</td>
-  <td>20</td>
```
```html
<tr v-for="(user, index) in users" :key="index">
  <td>{{user.name}}</td>
  <td>{{user.age}}</td>
```
```js
export default {
  computed: {
    users() {
      return this.$store.state.$users.users
    }
  },
  created() {
    this.$store.dispatch('usersRead')
  }
```

### Delete
src/store/usersModule.js
```js
  actions: {
    usersDelete(thisStore, index) {
      thisStore.state.users.splice(index, 1)
      console.log('Done usersDelete', thisStore.state.users)
    }
  }
```

src/components/contents/UsersComponent.vue (21줄)
```diff
- <button>Delete</button>
```
```html
<button @click="usersDelete(index)">Delete</button>
```
```js
export default {
  methods: {
    usersDelete(index) {
      this.$store.dispatch('usersDelete', index)
    }
```

### Update
src/store/usersModule.js
```js
  actions: {
    usersUpdate(thisStore, { index, user }) {
      thisStore.state.users[index] = user
      console.log('Done usersUpdate', thisStore.state.users)
    }
  }
```

src/components/contents/UsersComponent.vue (17줄)
```diff
- <td>{{user.name}}</td>
- <td>{{user.age}}</td>
- <td>
-  <button>Update</button>
```
```html
<td><input type="text" placeholder="Name" v-model="user.name" /></td>
<td><input type="text" placeholder="Age" v-model="user.age" /></td>
<td>
  <button @click="usersUpdate(index, user)">Update</button>
```
```js
export default {
  methods: {
    usersUpdate(index, user) {
      this.$store.dispatch('usersUpdate', { index, user })
    }
```

## Backend Server
* [Download](https://github.com/ovdncids/vue-curriculum/raw/master/download/express-server.zip)
```sh
# BE 서버 실행 방법
npm install
node index.js
# 터미널 종료
Ctrl + c
```

## Axios 서버 연동
https://github.com/axios/axios
```sh
npm install axios
```

### Read
src/store/index.js
```js
export default new Vuex.Store({
  actions: {
    axiosError(thisStore, error) {
      console.error(error.response || error.message || error)
      alert((error.response && error.response.statusText) || error.message || '알 수 없는 오류가 발생 하였습니다.')
    }
  }
```

src/store/usersModule.js
```js
import axios from 'axios'
```
```diff
  actions: {
    usersRead(thisStore) {
-     const users = [{
-       name: '홍길동',
-       age: 20
-     }, {
-       name: '춘향이',
-       age: 16
-     }]
-     thisStore.commit('usersRead', users)
-     console.log('Done usersRead', thisStore.state.users)
```
```js
      axios.get('http://localhost:3100/api/v1/users').then(function(response) {
        console.log('Done usersRead', response)
        thisStore.commit('usersRead', response.data.users)
      }).catch(function(error) {
        thisStore.dispatch('axiosError', error)
      })
```

### Create
src/store/usersModule.js
```diff
  actions: {
    usersCreate(thisStore, user) {
-     thisStore.state.users.push({
-       name: user.name,
-       age: user.age
-     })
-     console.log('Done usersCreate', thisStore.state.users)
```
```js
      axios.post('http://localhost:3100/api/v1/users', user).then(function(response) {
        console.log('Done usersCreate', response)
        thisStore.dispatch('usersRead')
      }).catch(function(error) {
        thisStore.dispatch('axiosError', error)
      })
```

### Delete
src/store/usersModule.js
```diff
  actions: {
    usersUpdate(thisStore, userUpdate) {
-     thisStore.state.users.splice(index, 1)
-     console.log('Done usersDelete', thisStore.state.users)
```
```js
      axios.delete('http://localhost:3100/api/v1/users/' + index).then(function(response) {
        console.log('Done usersDelete', response)
        thisStore.dispatch('usersRead')
      }).catch(function(error) {
        thisStore.dispatch('axiosError', error)
      })
```

### Update
src/store/usersModule.js
```diff
  actions: {
    usersUpdate(thisStore, { index, user }) {
-     thisStore.state.users[index] = user
-     console.log('Done usersRead', thisStore.state.users)
```
```js
      axios.patch('http://localhost:3100/api/v1/users/' + index, user).then(function(response) {
        console.log('Done usersUpdate', response)
        thisStore.dispatch('usersRead')
      }).catch(function(error) {
        thisStore.dispatch('axiosError', error)
      })
```

## Search Store 만들기
src/store/searchModule.js
```js
import axios from 'axios'

export const searchModule = {
  actions: {
    searchRead(thisStore, q) {
      const url = 'http://localhost:3100/api/v1/search?q=' + q
      axios.get(url).then(function(response) {
        console.log('Done searchRead', response)
        thisStore.commit('usersRead', response.data.users)
      }).catch(function(error) {
        thisStore.dispatch('axiosError', error)
      })
    }
  }
}
```

**searchModule.js를 Store에 등록**

src/store/index.js
```diff
+ import { searchModule } from './searchModule.js'

export default new Vuex.Store({
  modules: {
+   $search: searchModule
  }
```

## Search Component Vuex Store 주입
src/components/contents/SearchComponent.vue
```js
<template>
  <div>
    <h3>Search</h3>
    <hr class="d-block" />
    <div>
      <form>
        <input type="text" placeholder="Search">
        <button>Search</button>
      </form>
    </div>
    <hr class="d-block" />
    <div>
      <table class="table-search">
        <thead>
          <tr>
            <th>Name</th>
            <th>Age</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(user, key) in users" :key="key">
            <td>{{user.name}}</td>
            <td>{{user.age}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    users() {
      return this.$store.state.$users.users
    }
  },
  created() {
    this.$store.dispatch('searchRead', '')
  }
}
</script>
```

## Search Component에서만 사용 가능한 state값 적용
src/components/contents/SearchComponent.vue
```diff
-     <form>
-       <input type="text" placeholder="Search">
-       <button>Search</button>
-     </form>
```
```js
      <form @submit.prevent="searchRead()">
        <input type="text" placeholder="Search" v-model="q" />
        <button>Search</button>
      </form>
```
```js
export default {
  data() {
    return {
      q: ''
    }
  },
  methods: {
    searchRead() {
      this.$store.dispatch('searchRead', this.q)
    }
  },
}
```

## Search Component 쿼리스트링 변경
src/components/contents/SearchComponent.vue
```diff
  methods: {
    searchRead() {
-     this.$store.dispatch('searchRead', this.q)
+     this.$router.push({ name: 'Search', query: { q: this.q }})
    }
  },
```
`검색`, `뒤로가기` 해보기

## Search Component 새로고침 적용
```diff
  created() {
-   this.$store.dispatch('searchRead', '')  
+   this.q = this.$route.query.q || ''
+   this.$store.dispatch('searchRead', this.q)
  }
```
```js
export default {
  watch: {
    '$route.query': function(query, beforeQuery) {
      console.log(query, beforeQuery)
      this.q = query.q || ''
      this.$store.dispatch('searchRead', this.q)
    }
  },
```

## Proxy 설정
vue.config.js (파일 생성)
```js
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:3100'
      }
    }
  }
}
```

모든 파일 수정
```diff
- http://localhost:3100/api
+ /api
```

당황 하지 말고 다시 실행
```sh
npm run serve
```

# 수고 하셨습니다.
