# Script setup - Composition API

## Pinia
```sh
npm install pinia
```

src/plugins/index.js
```js
// Plugins
import vuetify from './vuetify'
import router from '@/router'
import { createPinia } from 'pinia'

// Pinia
const pinia = createPinia()

export function registerPlugins (app) {
  app
    .use(vuetify)
    .use(router)
    .use(pinia)
}
```

src/stores/usersStore.js
```js
import { defineStore } from 'pinia'

export const useUsersStore = defineStore('users', {
  state: () => ({
    users: [],
    user: {
      name: '',
      age: ''
    }
  }),
  actions: {
    usersCreate() {
      return this.user
    }
  }
})
```

src/pages/users.vue
```vue
<template>
  <form @submit.prevent="usersCreate()">
    <input type="text" placeholder="Name" v-model="usersStore.user.name" />
    <input type="text" placeholder="Age" v-model="usersStore.user.age" />
    <button>Create</button>
  </form>
  {{ usersStore.$state.users }}
  {{ usersRef }}
  {{ usersComputed }}
</template>

<script setup>
import { computed, ref, watch, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import { useUsersStore } from '@/stores/usersStore'

const route = useRoute()
const usersStore = useUsersStore()
console.log(route.path)
console.log(usersStore.user)

const usersCreate = () => {
  console.log(usersStore.usersCreate())
}

const usersComputed = computed(() => {
  return usersStore.$state.users
})
const usersRef = ref(usersComputed.value)

watch(usersComputed, (users) => {
  usersRef.value = users
})

onMounted(async () => {
  usersRef.value = await usersStore.usersCreate()
})
</script>
```
* ❕ `Pinia`는 `action`에서 `return`이 가능하다.

### 이전 형식과 setup이 공존할 경우
```vue
<template>
  {{ users }}
</template>

<script>
import { ref } from 'vue'
export default {
  setup() {
    const users = ref([])
    return {
      users
    }
  },
  async created() {
    this.users = [{}]
  }
}
</script>
```

### props
```vue
<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  propA: String,
  propB: {
    type: Number,
    default: 0
  }
})
</script>
```

### watchEffect
* [useEffect와 비슷하고 stop도 가능](https://kyounghwan01.github.io/blog/Vue/vue3/composition-api/#watch-watcheffect-%E1%84%8C%E1%85%AE%E1%86%BC%E1%84%8C%E1%85%B5)

## Vuex
```sh
npm install vuex
```

src/stores/index.js
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

src/plugins/index.js
```js
// Plugins
import vuetify from './vuetify'
import router from '@/router'
import { createStore } from 'vuex'
import { usersModule } from '@/stores/usersModule.js'

// Vuex
const store = createStore({
  modules: {
    $users: usersModule
  }
})

export function registerPlugins (app) {
  app
    .use(vuetify)
    .use(router)
    .use(store)
}
```

src/pages/users.vue
```vue
<template>
  <form @submit.prevent="usersCreate()">
    <input type="text" placeholder="Name" v-model="user.name" />
    <input type="text" placeholder="Age" v-model="user.age" />
    <button>Create</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'
import { useRoute } from 'vue-router'
import { useStore } from 'vuex'

const route = useRoute()
const store = useStore()
console.log(route.path)
console.log(store.state.$users.user.name)

const user = ref({
  name: '',
  age: ''
})
const usersCreate = () => {
  console.log(this.user.name)
  console.log(this.usersCreate)
}
</script>
```
