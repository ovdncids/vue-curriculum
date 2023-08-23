# ETC

## 이미지 부르기
```vue
<img :src="imgMain(img)" />

<script>
imgMain(img) {
  return require(`~/assets/imgs/${img}.png`)
}
</script>
```

## vuex-persistedstate
* https://github.com/robinvdvleuten/vuex-persistedstate
