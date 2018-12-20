# Vue.js

## Node.js
https://nodejs.org

## NVM (Node Version Manager)
Node.js 설치 버전을 관리하는 프로그램. 심볼릭 링크를 이용하여 Node.js 버전을 그때 그때 변경한다.
Node.js 버전 별로 자유롭게 설치, 이동, 삭제 가능하다. 현재는 Node.js v6, v8이 주류를 이룬다.

<!-- **Mac OS Node 삭제 방법**: https://gomugom.github.io/how-to-remove-node-from-macos/ -->

<!-- **VSCode에서 터미널 호출시 버전을 못 찾을 때**: https://github.com/Microsoft/vscode-docs/blob/master/docs/editor/integrated-terminal.md#why-is-nvm-complaining-about-a-prefix-option-when-the-integrated-terminal-is-launched
```sh
# nvm is not compatible with the npm config "prefix" option: currently set to "/usr/local"
# Run `npm config delete prefix` or `nvm use --delete-prefix v8.12.0 --silent` to unset it.
## nvm 설치 전에 npm이 설치되어서 문제가 발생 한다.
ls -la /usr/local/bin | grep npm
rm -R /usr/local/bin/npm /usr/local/lib/node_modules/npm/bin/npm-cli.js
``` -->

<!-- **nvm 삭제 방법**:
```sh
rm -rf ~/.nvm
rm -rf ~/.npm
rm -rf ~/.bower
``` -->

**Mac OS**: https://gist.github.com/falsy/8aa42ae311a9adb50e2ca7d8702c9af1
```sh
# 설치
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

# vi 에디터 실행
vi ~/.bash_profile

# 해당 경로 적용 시키키
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"

# ~/.bash_profile 재 실행 시키기
source ~/.bash_profile
```

**Windows**: https://github.com/coreybutler/nvm-windows/releases

```sh
# 설치 된 node.js 리스트를 본다.
nvm ls

# 해당 버전을 설치 한다.
nvm install 8.12.0

# 해당 버전을 삭제 한다.
nvm uninstall 8.12.0

# 해당 버전을 사용 한다.
nvm use 8.12.0

# 기본 버전 변경 하기
nvm alias default 8.12.0
```

## NPM (Node Package Manager)
```sh
# 상위 버전으로 업 한다. 현재 v6.4.1
npm install -g npm
```

<!-- ## Visual Studio Code
**Tab 스페이스 2칸으로 설정**: Preferences > 검색 > editor.detectIndent

https://stackoverflow.com/questions/29972396/how-to-set-tab-space-style

기본 텝 사이즈를 2칸으로 변경한다.
```json
"editor.tabSize": 2
```

해당 파일의 텝 사이즈를 무시하고 기본 텝 사이즈로 설정한다.
```json
"editor.detectIndentation": false
``` -->

## Vue CLI 3
https://kr.vuejs.org/v2/guide/index.html

https://cli.vuejs.org/guide

https://scotch.io/tutorials/creating-vue-apps-with-the-vue-ui-tool
```sh
# Vue CLI 3 설치
npm install -g @vue/cli

# Vue.js 프로젝트 생성
vue create vue-study
  # 생성이 안 될 경우
    npm install -g @vue/cli-service-global
  # 생성이 될 경우
    # Manually select features 선택
    # Babel, Router, Vuex, CSS Pre-processors, Linter / Formatter 선택
      # Test 필요시 Unit Testing 선택
    # Use history mode for router? Y 입력
    # Pick a CSS Pre-processor: Sass/SCSS 선택
    # ESLint with error prevention only 선택
    # Lint on save 선택
    # Mocha + Chai, Jest
      # Test를 선택 했을 경우 보여짐
        # Jest가 더 빠르므로 Jest 선택
          # --watchAll
    # In pacage.json 선택
    # Save this as a preset for future projects? N 입력
      # 현재 까지 선택 했던 사항을 별칭을 주어서 저장 할지 여부

# VSCode 해당 디렉토리 열기
# test
npm run test:unit
# build
npm run build
npm install -g serve
serve -s dist

# 프로젝트 실행
npm run serve
```

## 현재 문서 Git clone 하기

git clone https://github.com/ovdncids/vue-curriculum.git

## Git .gitignore
```sh
# npm or yarn
package-lock.json
yarn.lock

# .idea
.idea
```

**lock 파일**: 가끔 이 파일 때문에 클라이언트와 서버 사이에 버전이 안 맞아서 오류가 발생한다.
용량도 크고 npm install 할때 마다 생성되는 파일이니 .gitignore 목록에 넣는다.

**package-lock.json, yarn.lock 파일 삭제**

**Git push**
```sh
git push
```

**commit 이름 수정**
```sh
git commit --amend -m ""
```

**commit 취소**
```sh
git reset HEAD~
```

<!-- **첫 commit 취소**
```sh
git update-ref -d HEAD
``` -->

<!-- **이전 commit과 합치기**
```sh
git rebase -i HEAD~2
  # 2번째 줄 pick을 fixup으로 바꾸고 저장
``` -->

<!-- **이전으로 돌아가 수정 하기**
```sh
# 첫 commit 수정
git rebase -i --root $tip
# 이후 commit 수정
git rebase -i HEAD~2
  pick -> edit 수정
원하는 파일 수정
git add .
git rebase --continue
``` -->

**VSCode 확장 Git History 설치**

## Sass 설치
css를 프로그램화 하여 색상 테마를 변수에 넣을 수 있고, 반복 부분을 저장하고 불러 올 수 있다. 이름은 Sass지만 파일명은 scss이다.

https://sass-guidelin.es/ko/
```sh
npm install -D sass-loader node-sass
```

### 필요 없는 파일 지우기
```
src/assets/logo.png
src/views
src/components/HelloWorld.vue
```

src/App.vue
```html
<template>
  <div id="app">
  </div>
</template>
```

src/router.js
```
전부 주석 처리
```

## Markup
src/App.vue
```html
<template>
  <div id="app">
    <header><h1>Vue.js Study</h1></header>
    <hr />
    <div class="container">
      <div class="nav">
        <nav>
          <ul>
            <li><h2>CRUD</h2></li>
            <li><h2>Search</h2></li>
          </ul>
        </nav>
      </div>
      <hr />
      <div class="contents">
        <section>
          <div>
            <h3>CRUD</h3>
            <p>Contents</p>
          </div>
        </section>
      </div>
      <hr />
    </div>
    <footer>Copyright</footer>
  </div>
</template>

<script>
export default {
}
</script>

<style lang="scss">
@import "~@/assets/styles/App.scss";
</style>
```

src/assets/styles/App.scss
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

## CSS Flex
https://opentutorials.org/course/2418/13526

https://www.youtube.com/watch?v=eprXmC_j9A4

**현재 브라우저 상황**: YouTube IE11 부터 지원. IE11 부터 Flex 사용 가능. IE10은 Flex 부분 오류가 있어서 사용에 주의 해야 한다.

## Vue Component 만들기
Header.vue, Nav.vue, Contents.vue, Footer.vue 이렇게 Component 별로 파일을 나눈다.

src/App.vue
```js
import Header from './components/Header.vue'
import Nav from './components/container/Nav.vue'
import Contents from './components/container/Contents.vue'
import Footer from './components/Footer.vue'

export default {
  components: {
    Header,
    Nav,
    Contents,
    Footer
  }
}
```

기본 vue 파일
```html
<template>
  <div>
  </div>
</template>

<script>
export default {
}
</script>
```

## Vue props, v-show, v-if
src/App.vue
```html
// <Nav
v-show="true"

// <div class="contents"
v-if="true"

// <Footer
:title="'Copyright'"
```

src/components/Footer.vue
```html
<div @click="toggleShow()">
  <footer>{{title}} <span v-if="isShow">by</span></footer>
</div>
```
```js
export default {
  data() {
    return {
      isShow: true
    }
  },
  props: {
    title: {
      default: 'Rightcopy'
    }
  },
  methods: {
    toggleShow() {
      this.isShow = !this.isShow
    }
  }
}
```

## Vue router
src/App.vue
```diff
- <Contents></Contents>
+ <router-view></router-view>

- import Contents from './components/container/Contents.vue'

- Contents,

<!-- Contents.vue 파일 삭제 -->
```

src/components/container/contents/
```diff
- Contents.vue
+ contents/CRUD.vue

+ contents/Search.vue
```
src/routes.js
```diff
- import Home from './views/Home.vue'
+ import CRUD from './components/container/contents/CRUD.vue'

+ { path: '/', redirect: '/crud' },

- path: '',
- name: 'home',
- component: Home
+ path: '/crud',
+ name: 'crud',
+ component: CRUD

- path: '/about',
- name: 'about',
+ path: '/search',
+ name: 'search',

- component: () => import(/* webpackChunkName: "about" */ './views/About.vue')
+ // component: () => import(/* webpackChunkName: "about" */ './views/About.vue')
+ component: () => import('./components/container/contents/Search.vue')

```

src/components/container/Nav.vue
```html
<li><h2><router-link :to="{name: 'crud'}">CRUD</router-link></h2></li>
<li><h2><router-link :to="{path: '/search'}">Search</router-link></h2></li>
```

**여기 까지가 Markup 개발자 분들이 할일 입니다.**

## CRUD Conpenent Markup
src/components/container/contents/CRUD.vue
```html
<div>
  <h3>CRUD</h3>
  <hr class="d-block" />
  <div>
    <h4>Read</h4>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Age</th>
          <th>Created Date</th>
          <th>Modify</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>횽길동</td>
          <td>39</td>
          <td>2018-10-04</td>
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
```

## Vue Store 만들기
**Store 개념 설명**

Component는 상하, 수직, 부모 자식 관계인데 Store는 수평, 평등 관계이다.

**Vuex 설치**
src/shared/stores/types.js
```js
export const CRUD_CREATE = 'crud/CREATE'
```

src/shared/stores/modules/crudModule.js
```js
import * as types from '../types'

export const crudModule = {
  state: {
    member: {
      name: '',
      age: ''
    }
  },
  mutations: {
  },
  actions: {
    [types.CRUD_CREATE] ({ commit }) {
      console.log(types.CRUD_CREATE)
      console.log(crudModule.state.member)
    }
  }
}
```

**CRUD Store 등록하기**
src/shared/stores/store.js
```diff
- src/store.js
+ src/shared/stores/store.js
```
```js
import Vue from 'vue'
import Vuex from 'vuex'
import { crudModule } from './modules/crudModule'

Vue.use(Vuex)

export default new Vuex.Store({
  modules: {
    crud: crudModule
  }
})
```

src/main.js
```diff
- import store from './store'
+ import store from './shared/stores/store'
```

## error: Unexpected console statement (no-console) 해결
package.json
```json
"rules": {
  "no-console": "off"
}
```

안될 경우
```sh
vue add @vue/eslint
Error prevention only > Lint on save
```

## CRUD Conpenent Store inject
src/components/container/contents/CRUD.vue
```html
// <h4>Create</h4>  밑에
<input type="text" placeholder="Name" v-model="member.name" />
<input type="text" placeholder="Age" v-model="member.age" />
<button @click="create()">Create</button>
```
```js
import { mapState } from 'vuex'
import * as types from '../../../shared/stores/types'

export default {
  computed: {
    ...mapState({
      member: state => state.crud.member
    })
  },
  methods: {
    create() {
      this.$store.dispatch(types.CRUD_CREATE)
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

## Axios(서버 연동), toastr(메시지 창), spin.js(로딩 스피너), nprogress(프로그래스 바), lodash(배열, 오브젝트 유틸리티), moment(시간관련 유틸리티) 설치
```sh
npm install --save axios toastr spin.js nprogress lodash moment
```

## Validation with toastr
https://github.com/CodeSeven/toastr

src/shared/utils.js
```js
import Toastr from 'toastr'
import 'toastr/build/toastr.min.css'

export const toastr = () => {
  return Toastr
}
Toastr.options.closeButton = true
Toastr.options.hideDuration = 200
```

src/shared/stores/modules/crudModule.js
```js
import * as utils from '../utils'

// [types.CRUD_CREATE] () {
// validation
const member = crudModule.state.member
if (!member.name) {
  utils.toastr().warning('Please text your name.')
  return
}
if (!Number(member.age) || Number(member.age) <= 0) {
  utils.toastr().warning('Please text your age and upper than 0.')
  return
}
```

## Spin.js
https://spin.js.org/

src/shared/utils.js
```js
import { Spinner } from 'spin.js'
import 'spin.js/spin.css'

export const spinner = () => {
  return new Spinner({scale: 0.5})
}
```

src/components/container/contents/CRUD.vue
```html
<button class="relative pointer" @click="create($event.target)">Create</button>
```
```js
create(spinnerTarget) {
  this.$store.dispatch(types.CRUD_CREATE, { spinnerTarget, fromComponent: this })
}
```

src/shared/stores/modules/crudModule.js
```js
// [types.CRUD_CREATE] () {
[types.CRUD_CREATE] (commit, { spinnerTarget }) {
  utils.spinner().spin(spinnerTarget)
```

## node.js 서버 실행
```sh
npm install -g nodemon
nodemon index.js
```

## Axios 서버 연동
https://github.com/axios/axios

### Create
src/shared/utils.js
```js
export const apiCommonError = (error, spinner) => {
  console.log(error)
  console.log(error.response)
  const errMessage = (error.response && error.response.data && (error.response.data.message || error.response.data.errMessage || error.response.data.sqlMessage)) || error
  toastr().error(errMessage)
  if (spinner) {
    spinner.stop()
  }
}
```

src/shared/stores/modules/crudModule.js
```js
import axios from 'axios'

// [types.CRUD_CREATE] (commit, { spinnerTarget, fromComponent }) {
const spinner = utils.spinner().spin(spinnerTarget)
axios.post('http://localhost:3100/api/v1/member', member).then(response => {
  console.log(response)
  spinner.stop()
  utils.toastr().success(response.data.result)
}).catch(error => {
  utils.apiCommonError(error, spinner)
})
```

### Read
**nprogress**: https://github.com/rstacruz/nprogress

src/shared/utils.js
```js
import * as NProgress from 'nprogress'
import 'nprogress/nprogress.css'

// export const apiCommonError = (error, spinner) => {
nProgress.done()

export const nProgress = {
  start: () => NProgress.start(),
  done: () => NProgress.done()
}
```

src/shared/stores/types.js
```js
export const CRUD_READ = 'crud/READ'
```

src/shared/stores/modules/crudModule.js
```js
// state: {
members: []

// mutations: {
[types.CRUD_READ] (state, members) {
  state.members = members
}

// axios.post('http://localhost:3100/api/v1/member', member).then(response => {
fromComponent.$store.dispatch(types.CRUD_READ)

// actions: {
[types.CRUD_READ] ({ commit }) {
  utils.nProgress.start()
  axios.get('http://localhost:3100/api/v1/member').then(response => {
    console.log(response)
    commit(types.CRUD_READ, response.data.members)
    utils.nProgress.done()
  }).catch(error => {
    utils.apiCommonError(error)
  })
}
```

src/components/container/contents/CRUD.vue
```html
// <tbody>
<tr v-for="(member, key) in members" :key="key">
  <td>{{member.name}}</td>
  <td>{{member.age}}</td>
  <td>{{moment(member.createdDate).format('YYYY-MM-DD')}}</td>
```
```js
import moment from 'moment'

// computed: {
...mapState({
  member: state => state.crud.member,
  members: state => state.crud.members
}),
moment() {
  return moment
}

// created() {
this.$store.dispatch(types.CRUD_READ)
```

### Update
src/shared/stores/types.js
```js
export const CRUD_UPDATE = 'crud/UPDATE'
```

src/components/container/contents/CRUD.vue
```html
<td><input type="text" placeholder="Name" v-model="member.name" /></td>
<td><input type="text" placeholder="Age" v-model="member.age" /></td>

<button class="relative pointer" @click="update($event.target, key)">Update</button>
```
```js
// methods: {
update(spinnerTarget, key) {
  this.$store.dispatch(types.CRUD_UPDATE, { spinnerTarget, fromComponent: this, key })
}
```

src/shared/stores/modules/crudModule.js
```js
[types.CRUD_UPDATE] (commit, { spinnerTarget, fromComponent, key }) {
  const member = crudModule.state.members[key]
  if (!member.name) {
    utils.toastr().warning('Please text your name.')
    return
  }
  if (!Number(member.age) || Number(member.age) <= 0) {
    utils.toastr().warning('Please text your age and upper than 0.')
    return
  }
  const spinner = utils.spinner().spin(spinnerTarget)
  axios.put('http://localhost:3100/api/v1/member', {key, member}).then(response => {
    console.log(response)
    spinner.stop()
    utils.toastr().success(response.data.result)
    fromComponent.$store.dispatch(types.CRUD_READ)
  }).catch(error => {
    utils.apiCommonError(error, spinner)
  })
}
```

### Delete
src/shared/stores/types.js
```js
export const CRUD_DELETE = 'crud/DELETE'
```

src/components/container/contents/CRUD.vue
```html
<button class="relative pointer" @click="del($event.target, key)">Delete</button>
```
```js
del(spinnerTarget, key) {
  this.$store.dispatch(types.CRUD_DELETE, { spinnerTarget, fromComponent: this, key })
}
```

src/shared/stores/modules/crudModule.js
```js
[types.CRUD_DELETE] (commit, { spinnerTarget, fromComponent, key }) {
  if (!window.confirm('Are you sure?')) {
    return
  }
  const spinner = utils.spinner().spin(spinnerTarget)
  axios.delete(`http://localhost:3100/api/v1/member/${key}`).then(response => {
    console.log(response)
    spinner.stop()
    utils.toastr().success(response.data.result)
    fromComponent.$store.dispatch(types.CRUD_READ)
  }).catch(error => {
    utils.apiCommonError(error, spinner)
  })
}
```

## Search Conpenent Markup

src/components/container/contents/Search.vue
```html
<div>
  <h3>Search</h3>
  <hr class="d-block" />
  <div>
    <input type="text" />
    <button>Search</button>
  </div>
  <hr class="d-block" />
  <div>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Age</th>
          <th>Created Date</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>횽길동</td>
          <td>39</td>
          <td>2018-10-04</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
```

## Search Store 만들기

src/shared/stores/types.js
```js
export const SEARCH_READ = 'search/READ'
```

src/shared/stores/modules/searchModule.js
```js
import * as types from '../types'
import * as utils from '../../utils'
import axios from 'axios'

export const searchModule = {
  state: {
    member: {
      name: ''
    },
    members: []
  },
  mutations: {
    [types.SEARCH_READ] (state, members) {
      state.members = members
    }
  },
  actions: {
    [types.SEARCH_READ] ({ commit }) {
      utils.nProgress.start()
      axios.get('http://localhost:3100/api/v1/member').then(response => {
        console.log(response)
        commit(types.SEARCH_READ, response.data.members)
        utils.nProgress.done()
      }).catch(error => {
        utils.apiCommonError(error)
      })
    }
  }
}
```

**Search Store 등록하기**
src/shared/stores/store.js
```js
import { searchModule } from './modules/searchModule'

// modules: {
search: searchModule
```

## Search Conpenent Store inject
src/components/container/contents/Search.vue
```html
<input type="text" placeholder="Name" v-model="member.name" @keypress="keyPress($event)" />
<button class="relative pointer" @click="read()">Search</button>

// <tbody>
<tr v-for="(member, key) in members" :key="key">
  <td>{{member.name}}</td>
  <td>{{member.age}}</td>
  <td>{{moment(member.createdDate).format('YYYY-MM-DD')}}</td>
</tr>
```
```js
import { mapState } from 'vuex'
import * as types from '../../../shared/stores/types'
import moment from 'moment'

export default {
  computed: {
    ...mapState({
      member: state => state.search.member,
      members: state => state.search.members
    }),
    moment() {
      return moment
    }
  },
  methods: {
    read() {
      this.$store.dispatch(types.SEARCH_READ)
    },
    keyPress(e) {
      if (e.charCode === 13) {
        this.read()
      }
    }
  },
  created() {
    this.member.name = ''
    this.$store.dispatch(types.SEARCH_READ)
  }
}
```

## Search Conpenent 파라미터 변경과 새로고침 적용
src/components/container/contents/Search.vue
```js
// export default {
watch: {
  '$route.query': function (query, beforeQuery) {
    console.log(query, beforeQuery)
    this.member.name = query.name || ''
    this.$store.dispatch(types.SEARCH_READ)
  }
},

// read() {
this.$router.push({ name: 'search', query: { name: this.member.name }})

// created() {
this.member.name = this.$route.query.name || ''
```

## Proxy 설정

package.json
```json
"vue": {
  "devServer": {
    "proxy": "http://localhost:3100"
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
