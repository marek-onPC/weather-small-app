<template>
  <div class="home">
    <Search v-on:search-city="searchWeather"/>
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
