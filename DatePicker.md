# DatePicker

```sh
npm install moment
```

src/App.vue
```js
<div>
  <DatePicker :fromDates="fromDates"></DatePicker>
  {{fromDates}}
</div>

<script>
import moment from 'moment'
import DatePicker from './components/DatePicker.vue'

export default {
  components: {
    DatePicker
  },
  data() {
    return {
      fromDates: {
        startDate: moment().format('YYYY-MM-DD'),
        endDate: moment().add(2, 'weeks').format('YYYY-MM-DD')
      }
    }
  }
}
</script>
```

src/components/DatePicker.vue
```js
<template>
  <div>
    <input v-model="fromDates.startDate" @click="dpData.showDatePicker = !dpData.showDatePicker">
    ~ 
    <input v-model="fromDates.endDate" @click="dpData.showDatePicker = !dpData.showDatePicker">
    <div v-if="dpData.showDatePicker">
      <button @click="moveMonths(-1)">-1</button>
      <button @click="moveMonths(1)">1</button>
      <div class="date-picker-pair-calendar">
        <Calendar :fromDates="fromDates" :dpData="dpData" :isFirstCalendar="true"></Calendar>
        <Calendar :fromDates="fromDates" :dpData="dpData"></Calendar>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'
import Calendar from './Calendar.vue'

export default {
  components: {
    Calendar
  },
  props: {
    fromDates: Object
  },
  data() {
    return {
      dpData: {
        showDatePicker: false,
        selectedYearMonth: moment(this.fromDates.startDate).format('YYYY-MM')
      }
    }
  },
  watch: {
    'dpData.showDatePicker': function(showDatePicker) {
      if (showDatePicker) {
        this.dpData.selectedYearMonth = moment(this.fromDates.startDate).format('YYYY-MM')
      }
    }
  },
  methods: {
    moveMonths(value) {
      this.dpData.selectedYearMonth = moment(this.dpData.selectedYearMonth).add(value, 'months').format('YYYY-MM')
      console.log(this.dpData.selectedYearMonth)
    }
  }
}
</script>

<style>
.date-picker-pair-calendar {
  display: flex;
}
</style>
```

src/components/Calendar.vue
```js
<template>
  <div>
    {{currentYearMonth}}
    <!-- <button @click="fromDates.startDate = '2021-01-01'">2021-01-01</button> -->
    <div>
      <table>
        <thead>
          <tr>
            <th>Sun</th>
            <th>Mon</th>
            <th>Tue</th>
            <th>Wen</th>
            <th>Thu</th>
            <th>Fri</th>
            <th>Sat</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="line in 5" :key="line">
            <td v-for="day in 7" :key="day">{{calcDay(line, day)}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  props: {
    fromDates: Object,
    dpData: Object,
    isFirstCalendar: Boolean
  },
  computed: {
    currentYearMonth() {
      return this.isFirstCalendar
        ? this.dpData.selectedYearMonth
        : moment(this.dpData.selectedYearMonth).add(1, 'months').format('YYYY-MM')
    },
    firstDay() {
      return moment(this.currentYearMonth).startOf('month')
    }
  },
  methods: {
    calcDay(line, day) {
      const calc = (line - 1) * 7 + (day - 1) - this.firstDay.day()
      return moment(this.firstDay).add(calc, 'days').format('D')
    }
  },
  created() {
    console.log('move')
  }
}
</script>
```
