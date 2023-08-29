# Nuxt.js
* 주로 Vue.js의 SPA(Single page application)의 단점인 SEO(Search engine optimization)을 해결하기 위해 사용한다.
* Express 서버의 SSR(Server side rendering)과, Vue.js의 CSR(Client side rendering)을 혼합하여 사용해서, SEO를 해결 한다.

## 설치
```sh
# Nuxt 프로젝트 생성
npx create-nuxt-app nuxt-study
  Project name: nuxt-study
  Programming language: JavaScript
  Package manager: Npm
  UI framework: None
  Template engine: HTML
  Nuxt.js modules: Axios - Promise based HTTP client <-선택
  Linting tools: Commitlint (https://github.com/conventional-changelog/commitlint/#what-is-commitlint)
  Testing framework: None or Jest
  Rendering mode: Universal (SSR / SSG)
  Deployment target: Server (Node.js hosting)
  Development tools: jsconfig.json (Recommended for VS Code if you're not using typescript)
  Continuous integration: None
  Version control system: Git

cd nuxt-study
code .

# 결과물을 .nuxt 경로에 build 한다.
npm run build
# build된 .nuxt 경로를 로컬 서버로 띄운다.
npm run start

# 로컬 개발 서버를 띄운다.
npm run dev
```

## Markup
components/layouts/layout.vue
```vue
<template>
  <div>
    <layout-header />
    <hr />
    <div class="container">
      <layout-nav />
      <hr />
      <section class="contents">
        <nuxt />
      </section>
      <hr />
    </div>
    <layout-footer>Copyright</layout-footer>
  </div>
</template>

<script>
import Vue from 'vue'
import LayoutHeader from './header.vue'
import LayoutNav from './nav.vue'
import LayoutFooter from './footer.vue'
import '~/style/index.css'

export default {
  components: {
    LayoutHeader,
    LayoutNav,
    LayoutFooter
  }
}
</script>
```

layouts/header.vue
```vue
<template>
  <header>
    <h1>Vue.js study</h1>
  </header>
</template>
```

layouts/nav.vue
```vue
<template>
  <nav class="nav">
    <ul>
      <li>
        <h2><nuxt-link to="/">Home</nuxt-link></h2>
      </li>
      <li>
        <h2><nuxt-link to="/users">Users</nuxt-link></h2>
      </li>
      <li>
        <h2><nuxt-link to="/search">Search</nuxt-link></h2>
      </li>
    </ul>
  </nav>
</template>
```

layouts/footer.vue
```vue
<template>
  <footer>Copyright</footer>
</template>
```

style/index.css
```css
* {
  margin: 0;
  font-family: -apple-system,BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}
a:link, a:visited {
  text-decoration: none;
  color: black;
}
a.active,
a.nuxt-link-exact-active {
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

## Users Store
### Read
store/usersStore.js
```js
export const state = () => ({
  users: []
})

export const mutations = {
  usersRead(state, users) {
    state.users = users
  }
}

export const actions = {
  async usersRead({ commit }, context) {
    try {
      await context.$axios.get('http://localhost:3100/api/v1/users')
      commit('usersRead', response.data.users)
    } catch (error) {}
  }
}
```

<!--
#### Missing space before function parentheses space-before-function-paren 발생할 경우
.eslintrc.js
```js
rules: {
  'space-before-function-paren': ['error', 'never']
}
```
#### Expected parentheses around arrow function argument having a body with curly braces  arrow-parens 발생할 경우
```js
rules: {
  'arrow-parens': 0
}
```
#### vue/mustache-interpolation-spacing
```js
rules: {
  'vue/mustache-interpolation-spacing': ['error', 'never']
}
```
-->

pages/users.vue
```vue
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
          <tr v-for="(user, index) in users" :key="index">
            <td>{{user.name}}</td>
            <td>{{user.age}}</td>
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
  async asyncData(context) {
    await context.store.dispatch('usersStore/usersRead', context)
  },
  computed: {
    users() {
      return this.$store.state.usersStore.users
    }
  },
  // async created() {
  //   debugger
  //   await this.$store.dispatch('usersStore/usersRead', this)
  // }
}
</script>
```
* ❕ `asyncData`, `created` 함수 모두 `SSR`에서 동작 하지만 `created`는 async await 도중에 페이지가 그려진다.
* ❕ `pages 폴더` 안에서만 `asyncData` 함수 사용 가능하다.
* `Nav 메뉴`에서 router 이동 후 돌아 온다면, `CSR`쪽에서 `asyncData`, `created` 함수가 실행 된다.
* `IE11`에서도 별도의 `Polyfill`없이 `async, await` 사용 가능 하다.

### Create
* ❕ `store.state`는 `commit함수`를 통해서만 수정 가능하다.

pages/users.vue
```vue
<input type="text" placeholder="Name" v-model="user.name" />
<input type="text" placeholder="Age" v-model="user.age" />
<button @click="usersCreate(user)">Create</button>
```
```vue
data() {
  return {
    user: {
      name: '',
      age: ''
    }
  }
},
methods: {
  usersCreate(user) {
    this.$store.dispatch('usersStore/usersCreate', {
      context: this,
      user
    })
  }
}
```

store/usersStore.js
```js
async usersCreate({ dispatch }, { context, user }) {
  try {
    await context.$axios.post('http://localhost:3100/api/v1/users', user)
    dispatch('usersRead', context)
  } catch (error) {}
}
```

### Delete
pages/users.vue
```vue
<button @click="usersDelete(index)">Delete</button>
```
```vue
usersDelete(index) {
  this.$store.dispatch('usersStore/usersDelete', {
    context: this,
    index
  })
}
```

store/usersStore.js
```js
async usersDelete({ dispatch }, { context, index }) {
  try {
    await context.$axios.delete('http://localhost:3100/api/v1/users/' + index)
    dispatch('usersRead', context)
  } catch (error) {}
}
```

### Update
pages/users.vue
```vue
<td><input type="text" placeholder="Name" v-model="user.name" /></td>
<td><input type="text" placeholder="Age" v-model="user.age" /></td>
<td>
  <button @click="usersUpdate(index, user)">Update</button>
```
```vue
computed: {
  users() {
    return [
      ...JSON.parse(JSON.stringify(this.$store.state.usersStore.users))
    ]
  }
},
```
```vue
usersUpdate(index, user) {
  this.$store.dispatch('usersStore/usersUpdate', {
    context: this,
    index,
    user
  })
}
```

store/usersStore.js
```js
async usersUpdate({ dispatch }, { context, index, user }) {
  try {
    await context.$axios.patch('http://localhost:3100/api/v1/users/' + index, user)
    dispatch('usersRead', context)
  } catch (error) {}
}
```

## Search
pages/users.vue
```vue
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
  async asyncData(context) {
    await context.store.dispatch('searchStore/searchRead', {
      commit: this.$store.commit,
      context,
      q: ''
    })
  },
  computed: {
    users() {
      return this.$store.state.usersStore.users
    }
  }
}
</script>
```

store/searchStore.js
```js
export const actions = {
  async searchRead(_, { commit, context, q }) {
    try {
      const response = await context.$axios.get('http://localhost:3100/api/v1/search?q=' + q)
      commit('usersStore/usersRead', response.data.users)
    } catch (error) {}
  }
}
```

### Search Component에서만 사용 가능한 state값 적용
pages/users.vue
```vue
<form @submit.prevent="searchRead()">
  <input type="text" placeholder="Search" v-model="q" />
  <button>Search</button>
</form>
```
```vue
data() {
  return {
    q: ''
  }
},
methods: {
  searchRead() {
    this.$store.dispatch('searchStore/searchRead', {
      commit: this.$store.commit,
      context: this,
      q: this.q
    })
  }
}
```

# Promise.all
```js
async asyncData() {
  const getMyCars = myCarService.getMyCars()
  const getProducts = repairService.getProducts()
  const getItems = repairService.getItems()
  const [myCars, products, items] = await Promise.all([getMyCars, getProducts, getItems])
  return {
    myCars: myCars.myCars,
    products,
    items
  }
}
```
* ❕ `return`의 `{}` 부분이 `this(data)` 안으로 자동으로 들어가게 된다.

# Vite
* https://vite.nuxtjs.org/getting-started/installation
```sh
// Nuxt@2.15.8
npm install -D nuxt-vite@0.2.4
```

nuxt.config.js
```js
export default {
  buildModules: [
    'nuxt-vite'
  ],
  vite: {
    ssr: true
  }
}
```

## Cannot find module 'lib/axios'
* https://github.com/nuxt/vite/issues/221
