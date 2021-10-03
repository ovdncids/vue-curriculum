# Hightcharts
* https://github.com/highcharts/highcharts-vue

```sh
npm install highcharts highcharts-vue
```

src/main.js
```js
import HighchartsVue from 'highcharts-vue'
Vue.use(HighchartsVue)
```

src/App.vue
```vue

<script>
<highcharts :options="chartOptions"></highcharts>

export default {
  data() {
    return {
      chartOptions: {
        xAxis: {
          categories: ['2021-01-01', '2021-09-01', '2021-09-30']
        },
        series: [{
          data: [1, 2, 3]
        }]
      }
    }
  }
}
</script>
```
