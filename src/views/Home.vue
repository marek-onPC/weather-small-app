<template>
<div class="home">
  <Search v-on:search-city="searchWeather"/>
  <div class="mdl-grid">
    <div class="mdl-cell mdl-cell--8-col mdl-cell--12-col-tablet">WEATHER ICON + DESCRIPTION</div>
    <div class="mdl-cell mdl-cell--4-col mdl-cell--12-col-tablet">TEMP + FEELS LIKE TEMP</div>
    <div class="mdl-cell mdl-cell--6-col mdl-cell--12-col-tablet">MAX/MIN TEMP</div>
    <div class="mdl-cell mdl-cell--6-col mdl-cell--12-col-tablet">RAIN/SNOW</div>
    <div class="mdl-cell mdl-cell--4-col mdl-cell--2-col-phone">HUMIDITY</div>
    <div class="mdl-cell mdl-cell--4-col mdl-cell--2-col-phone">PRESSURE</div>
    <div class="mdl-cell mdl-cell--4-col mdl-cell--12-col-tablet">WIND</div>
  </div>
</div>
</template>

<script>
// @ is an alias to /src
import Search from '@/components/Search.vue'
const axios = require('axios').default

export default {
  name: 'Home',
  components: {
    Search
  },
  data () {
    return {
      weatherAPI: '75f9685f116b28f3c9b5ad6246d906ae',
      weatherData: []
    }
  },
  methods: {
    searchWeather (value) {
      return axios.get('https://api.openweathermap.org/data/2.5/weather?q=' + value + '&units=metric&appid=' + this.weatherAPI)
        .then(response => {
          console.log(response.data)
          this.weatherData = response.data
          return response.data
        })
        .catch(error => {
          console.log(error)
          setTimeout(() => {
            this.searchWeather()
          }, 1500)
        })
    }
  }
}
</script>

<style lang="scss" scoped>
.mdl {
  &-grid {
    max-width: 1000px;
    margin-top: 50px;
  }
}
</style>
