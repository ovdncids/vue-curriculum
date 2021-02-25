# Vue.js

## Node.js
https://nodejs.org

## NVM (Node Version Manager)
Node.js 버전을 관리하는 프로그램, 어느 버전이든 설치, 변경, 삭제 가능하다.

<details><summary>Mac OS</summary>
https://github.com/nvm-sh/nvm

https://gist.github.com/falsy/8aa42ae311a9adb50e2ca7d8702c9af1
```sh
# 설치
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash

# vi 에디터 실행
vi ~/.bash_profile

# 해당 경로 적용 시키키
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

# ~/.bash_profile 재 실행 시키기
source ~/.bash_profile
```
</details>

Windows

https://github.com/coreybutler/nvm-windows/releases

```sh
# 설치 된 node.js 리스트를 본다.
nvm ls

# 해당 버전을 설치 한다.
nvm install 14.15.5

# 해당 버전을 삭제 한다.
nvm uninstall 14.15.5

# 해당 버전을 사용 한다.
nvm use 14.15.5

# 기본 버전 변경 하기
nvm alias default 14.15.5
```

## Vue CLI
https://kr.vuejs.org/v2/guide/index.html

https://cli.vuejs.org/guide/installation.html
```sh
# Vue CLI 설치
npm install -g @vue/cli

# Vue.js 프로젝트 생성
vue create vue-study
## Normal type without Test ([Vue 2] dart-sass, babel, router, vuex, eslint) 선택

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
          <li><h2>Members</h2></li>
          <li><h2>Search</h2></li>
        </ul>
      </nav>
      <hr />
      <section class="contents">
        <div>
          <h3>Members</h3>
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
body {
  margin: 0;
}

// common
.pointer {
  cursor: pointer;
}

.relative {
  position: relative;
}

.d-none {
  display: none;
}

.d-block {
  display: block;
}

.flex {
  display: flex;
}

// Markup
hr {
  display: none;
}

h1, footer {
  margin: 0.5rem;
}

.container {
  @extend .flex;
  min-height: 300px;
  border-top: 1px solid #ddd;
  border-bottom: 1px solid #ddd;
  .nav {
    min-height: 300px;
    background-color: skyblue;
    ul {
      list-style: none;
      margin: 0.5rem 0 0.5rem 0;
      padding: 0;
      h2 {
        margin: 0;
        padding: 0.5rem;
      }
    }
  }
  .contents {
    margin-left: 1rem;
  }
}
```

src/main.js (App.scss 부르기)
```js
import "@/assets/scss/App.scss"
```

## Vue Component 만들기
Header.vue, Nav.vue, Contents.vue, Footer.vue 이렇게 Component 별로 파일을 나눈다.

src/App.vue
```html
<!-- 가장 아래에 추가 -->
<script>
import Header from './components/Header.vue'
import Nav from './components/Nav.vue'
import Footer from './components/Footer.vue'

export default {
  components: {
    Header,
    Nav,
    Footer
  }
}
</script>
```

기본 .vue 파일
```html
<template>
  <div></div>
</template>

<script>
export default {
}
</script>
```

src/App.vue
```diff
- <header>
-  <h1>Vue.js study</h1>
- </header>
+ <Header></Header>

- <nav class="nav">
-   <ul>
-     <li><h2>Members</h2></li>
-     <li><h2>Search</h2></li>
-   </ul>
- </nav>
+ <Nav></Nav>

- <footer>Copyright</footer>
+ <Footer></Footer>
```


## v-show, v-if, props
src/App.vue
```html
<Header v-show="false"></Header>

<Nav v-if="false"></Nav>

<Footer :title="'카피라이트'"></Footer>
```

src/components/Footer.vue
```html
<footer>{{title}}</footer>
```
```js
export default {
  props: {
    title: {
      default: 'Copyright'
    }
  }
}
```
**props는 부모 Component에서 자식 Component로 값을 전달 한다**

## Vue router
src/App.vue (Contents 태그를 router-view 태그로 변경)
```diff
<template>
  <section class="contents">
-   <div>
-     <h3>Members</h3>
-     <p>Contents</p>
-   </div>
+   <router-view></router-view>
```

src/components/contents/Members.vue
```html
<template>
  <div>
    <h3>Members</h3>
    <p>Contents</p>
  </div>
</template>
```

src/router/index.js (3줄 부터 21줄 까지 덮어 씌우기)
```diff
- import Home from '../views/Home.vue'
- ...
- ]
```
```js
import Members from '../components/contents/Members.vue'
import Search from '../components/contents/Search.vue'

Vue.use(VueRouter)

const routes = [
  { path: '/', redirect: '/members' },
  {
    path: '/members',
    name: 'Members',
    component: Members
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

src/components/Nav.vue (li 태그 부분 덮어 씌우기)
```html
<li><h2><router-link :to="{name: 'Members'}">Members</router-link></h2></li>
<li><h2><router-link :to="{path: '/search'}">Search</router-link></h2></li>
```

**여기 까지가 Markup 개발자 분들이 할일 입니다.**

## Members Store 만들기
**Store 개념 설명**

Component가 사용하는 글로벌 함수 또는 변수라고 생각하면 쉽다, store 값이 변하면 해당 값을 바라 보는 모든 Component가 수정 된다.

src/store/moduleMembers.js
```js
export const moduleMembers = {
  state: {
    members: [],
    member: {
      name: '',
      age: ''
    }
  },
  mutations: {
  },
  actions: {
    membersCreate(thisStore) {
      thisStore.state.members.push({
        name: thisStore.state.member.name,
        age: thisStore.state.member.age
      })
      console.log('Done membersCreate', moduleMembers.state.members)
    }
  }
}
```

**moduleMembers.js를 Store에 등록하기**

src/store/index.js
```diff
+ import { moduleMembers } from './moduleMembers.js'

export default new Vuex.Store({
  modules: {
+   members: moduleMembers
```

## Members Component Store inject
src/components/contents/Members.vue
```html
<template>
  <div>
    <h3>Members</h3>
    <hr class="d-block" />
    <div>
      <h4>Read</h4>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Age</th>
            <th>Update</th>
            <th>Delete</th>
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
      <input type="text" placeholder="Name" v-model="member.name" />
      <input type="text" placeholder="Age" v-model="member.age" />
      <button @click="membersCreate()">Create</button>
    </div>
  </div>
</template>
```

```js
export default {
  computed: {
    member() {
      return this.$store.state.members.member
    }
  },
  methods: {
    membersCreate() {
      this.$store.dispatch('membersCreate')
    }
  },
  created() {
    this.member.name = ''
    this.member.age = ''
  }
}
```

**computed, methods 차이 설명**

**debugger 설명**
```js
debugger
```

## Members Store CRUD
### Read
src/store/moduleMembers.js
```js
  mutations: {
    membersRead(state, members) {
      state.members = members
    }
  actions: {
    membersRead(thisStore) {
      const members = [{
        name: '홍길동',
        age: 20
      }, {
        name: '춘향이',
        age: 16
      }]
      thisStore.commit('membersRead', members)
      console.log('Done membersRead', moduleMembers.state.members)
    }
```

src/components/contents/Members.vue (17줄)
```diff
- <tr>
-  <td>홍길동</td>
-  <td>20</td>
```
```html
<tr v-for="(member, index) in members" :key="index">
  <td>{{member.name}}</td>
  <td>{{member.age}}</td>
```
```js
export default {
  computed: {
    members() {
      return this.$store.state.members.members
    }
  created() {
    this.$store.dispatch('membersRead')
```

### Update
src/store/moduleMembers.js
```js
  actions: {
    membersUpdate(thisStore, memberUpdate) {
      thisStore.state.members[memberUpdate.index] = memberUpdate.member
      console.log('Done membersUpdate', moduleMembers.state.members)
    }
```

src/components/contents/Members.vue (18줄)
```diff
- <td>{{member.name}}</td>
- <td>{{member.age}}</td>
- <td>
-  <button>Update</button>
```
```html
<td><input type="text" placeholder="Name" v-model="member.name" /></td>
<td><input type="text" placeholder="Age" v-model="member.age" /></td>
<td>
  <button @click="membersUpdate(index, member)">Update</button>
```
```js
export default {
  methods: {
    membersUpdate(index, member) {
      this.$store.dispatch('membersUpdate', {
        index: index,
        member: member
      })
    }
```

### Delete
src/store/moduleMembers.js
```js
  actions: {
    membersDelete(thisStore, index) {
      thisStore.state.members.splice(index, 1)
      console.log('Done membersDelete', moduleMembers.state.members)
    }
```

src/components/contents/Members.vue (24줄)
```diff
- <button>Delete</button>
```
```html
<button @click="membersDelete(index)">Delete</button>
```
```js
export default {
  methods: {
    membersDelete(index) {
      this.$store.dispatch('membersDelete', index)
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

### Create
src/store/index.js
```js
export default new Vuex.Store({
  actions: {
    axiosError(thisStore, error) {
      console.error(error.response || error.message || error)
    }
```

src/store/moduleMembers.js
```js
import axios from 'axios'
```
```diff
  actions: {
    membersCreate(thisStore) {
-     thisStore.state.members.push({
-       name: thisStore.state.member.name,
-       age: thisStore.state.member.age
-     })
-     console.log('Done membersCreate', moduleMembers.state.members)
```
```js
      axios.post('http://localhost:3100/api/v1/members', thisStore.state.member).then(function(response) {
        console.log('Done membersCreate', response)
        thisStore.dispatch('membersRead')
      }).catch(function(error) {
        thisStore.dispatch('axiosError', error)
      })
```

### Read
src/store/moduleMembers.js
```diff
  actions: {
    membersRead(thisStore) {
-     const members = [{
-       name: '홍길동',
-       age: 20
-     }, {
-       name: '춘향이',
-       age: 16
-     }]
-     thisStore.commit('membersRead', members)
-     console.log('Done membersRead', moduleMembers.state.members)
```
```js
      axios.get('http://localhost:3100/api/v1/members').then(function(response) {
        console.log('Done membersRead', response)
        thisStore.commit('membersRead', response.data.members)
      }).catch(function(error) {
        thisStore.dispatch('axiosError', error)
      })
```

### Update
src/store/moduleMembers.js
```diff
  actions: {
    membersUpdate(thisStore, memberUpdate) {
-     thisStore.state.members[memberUpdate.index] = memberUpdate.member
-     console.log('Done membersRead', moduleMembers.state.members)
```
```js
      axios.patch('http://localhost:3100/api/v1/members', memberUpdate).then(function(response) {
        console.log('Done membersUpdate', response)
        thisStore.dispatch('membersRead')
      }).catch(function(error) {
        thisStore.dispatch('axiosError', error)
      })
```

### Delete
src/store/moduleMembers.js
```diff
  actions: {
    membersUpdate(thisStore, memberUpdate) {
-     thisStore.state.members.splice(index, 1)
-     console.log('Done membersDelete', moduleMembers.state.members)
```
```js
      axios.delete('http://localhost:3100/api/v1/members/' + index).then(function(response) {
        console.log('Done membersDelete', response)
        thisStore.dispatch('membersRead')
      }).catch(function(error) {
        thisStore.dispatch('axiosError', error)
      })
```

## Search Store 만들기
src/shared/stores/modules/moduleSearch.js
```js
import axios from 'axios'

export const moduleSearch = {
  actions: {
    searchRead(thisStore, search) {
      const url = 'http://localhost:3100/api/v1/search?search=' + search
      axios.get(url).then(function(response) {
        console.log('Done searchRead', response)
        thisStore.commit('membersRead', response.data.members)
      }).catch(function(error) {
        thisStore.dispatch('axiosError', error)
      })
    }
  }
}
```

**moduleSearch.js를 Store에 등록하기**

src/store/index.js
```diff
+ import { moduleSearch } from './moduleSearch.js'

export default new Vuex.Store({
  modules: {
+   search: moduleSearch
```

## Search Component Store inject
src/components/contents/Search.vue
```html
<template>
  <div>
    <h3>Search</h3>
    <hr class="d-block" />
    <div>
      <input type="text" placeholder="Search" v-model="search" @keyup="keyUp($event)" />
      <button @click="searchRead()">Search</button>
    </div>
    <hr class="d-block" />
    <div>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Age</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(member, key) in members" :key="key">
            <td>{{member.name}}</td>
            <td>{{member.age}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
```
```js
export default {
  data() {
    return {
      search: ''
    }
  },
  computed: {
    members() {
      return this.$store.state.members.members
    }
  },
  methods: {
    keyUp($event) {
      if ($event.key === 'Enter') this.searchRead()
    },
    searchRead() {
      this.$store.dispatch('searchRead', this.search)
    }
  },
  created() {
    this.$store.dispatch('searchRead', this.search)
  }
}
```

## Search Component 파라미터 변경과 새로고침 적용
src/components/contents/Search.vue
```js
export default {
  watch: {
    '$route.query': function (query, beforeQuery) {
      console.log(query, beforeQuery)
      this.search = query.search || ''
      this.$store.dispatch('searchRead', this.search)
    }
  }
```
```diff
  methods: {
    searchRead() {
-     this.$store.dispatch('searchRead', this.search)
+     this.$router.push({ name: 'Search', query: { search: this.search }})
  created() {
+   this.search = this.$route.query.search || ''
```

## Proxy 설정
/vue.config.js (파일 생성)
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

모든 파일 수정 하기
```diff
- http://localhost:3100/api
+ /api
```

당황 하지 말고 다시 실행 하기
```sh
npm run serve
```

# 수고 하셨습니다.
