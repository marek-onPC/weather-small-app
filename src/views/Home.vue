<template>
<div class="home">
  <Search v-on:search-city="searchWeather"/>
  <div class="mdl-grid" v-if="weatherData !== ''">
    <div class="mdl-cell mdl-cell--4-col mdl-cell--12-col-tablet">
      <div class="mdl-card mdl-shadow--2dp">
        <div class="mdl-card__title mdl-card--expand">
          <h2 class="mdl-card__title-text">{{ weatherData.name }}</h2>
          <img :src="`http://openweathermap.org/img/wn/${ weatherData.weather[0].icon }@2x.png`" alt="">
        </div>
        <div class="mdl-card__supporting-text">
          <strong>{{ weatherData.weather[0].description }}</strong> - {{ weatherData.dt }}
        </div>
      </div>
    </div>
    <div class="mdl-cell mdl-cell--8-col mdl-cell--12-col-tablet">
      <div class="mdl-card mdl-shadow--2dp">
        <div class="mdl-card__title mdl-card--expand">
          <p class="mdl-card__title-text">Now: {{ weatherData.main.temp }} °C</p>
          <p class="mdl-card__title-text">Real feel: {{ weatherData.main.feels_like }} °C</p>
        </div>
        <div class="mdl-card__supporting-text">
          <strong>Temperatures</strong>
        </div>
      </div>
    </div>
    <div class="mdl-cell mdl-cell--6-col mdl-cell--12-col-tablet">
      <div class="mdl-card mdl-shadow--2dp">
        <div class="mdl-card__title mdl-card--expand">
          <p class="mdl-card__title-text">Max: {{ weatherData.main.temp_max }} °C</p>
          <p class="mdl-card__title-text">Min: {{ weatherData.main.temp_min }} °C</p>
        </div>
        <div class="mdl-card__supporting-text">
          <strong>Temperatures</strong>
        </div>
      </div>
    </div>
    <div class="mdl-cell mdl-cell--6-col mdl-cell--12-col-tablet" v-if="weatherData.rain || weatherData.snow">
      <div class="mdl-card mdl-shadow--2dp">
        <div class="mdl-card__title mdl-card--expand">
          <p class="mdl-card__title-text" v-if="weatherData.rain">Rain: {{ weatherData.rain['1h'] }} mm<sup>2</sup>/h</p>
          <p class="mdl-card__title-text" v-if="weatherData.snow">Snow: {{ weatherData.snow['1h'] }} mm<sup>2</sup>/h</p>
        </div>
        <div class="mdl-card__supporting-text">
          <strong>Rain & Snow</strong>
        </div>
      </div>
    </div>
    <div class="mdl-cell mdl-cell--4-col mdl-cell--2-col-phone">
      <div class="mdl-card mdl-shadow--2dp">
        <div class="mdl-card__title mdl-card--expand">
          <p class="mdl-card__title-text">{{ weatherData.main.humidity }} %</p>
        </div>
        <div class="mdl-card__supporting-text">
          <strong>Humidity</strong>
        </div>
      </div>
    </div>
    <div class="mdl-cell mdl-cell--4-col mdl-cell--2-col-phone">
      <div class="mdl-card mdl-shadow--2dp">
        <div class="mdl-card__title mdl-card--expand">
          <p class="mdl-card__title-text">{{ weatherData.main.pressure }} hPa</p>
        </div>
        <div class="mdl-card__supporting-text">
          <strong>Pressure</strong>
        </div>
      </div>
    </div>
    <div class="mdl-cell mdl-cell--4-col mdl-cell--12-col-tablet">
      <div class="mdl-card mdl-shadow--2dp">
        <div class="mdl-card__title mdl-card--expand">
          <p class="mdl-card__title-text">{{ weatherData.wind.speed }} m/s</p>
        </div>
        <div class="mdl-card__supporting-text">
          <strong>Wind speed</strong>
        </div>
      </div>
    </div>
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
      weatherData: ''
    }
  },
  methods: {
    searchWeather (value) {
      return axios.get('https://api.openweathermap.org/data/2.5/weather?q=' + value + '&units=metric&appid=' + this.weatherAPI)
        .then(response => {
          console.log(response.data)
          this.weatherData = response.data

          // Based on curret timestamp prepared with Data() class and city's timestamp, we can calculate current time in searched city
          var currentTime = new Date(new Date().getTime() + new Date().getTimezoneOffset() * 60000 + response.data.timezone * 1000)
          var currentTimeHours = currentTime.getHours()
          var currentTimeMinutes = '0' + currentTime.getMinutes()
          this.weatherData.dt = currentTimeHours + ':' + currentTimeMinutes.substr(-2)

          return response.data
        })
        .catch(error => {
          console.log(error)
          setTimeout(() => {
            this.searchWeather()
          }, 1500)
        })
    },
    refreshMDL () {
      if (typeof componentHandler !== 'undefined') {
        window.componentHandler.upgradeAllRegistered()
      }
    }
  },
  mounted () {
    this.refreshMDL()
  }
}
</script>

<style lang="scss" scoped>
.mdl {
  &-grid {
    max-width: 1000px;
    margin-top: 50px;
    justify-content: center;
  }

  &-card {
    width: 100%;

    &__title {
      justify-content: space-evenly;

      &-text {
        font-size: 32px;
        font-weight: 500;
        text-shadow: 1px 1px 2px #777;
        padding-bottom: 40px;
      }

      img {
        transform: scale(1.25);
        filter: drop-shadow(1px 2px 2px #777);
      }
    }

    &__supporting-text {
      font-size: 18px;
      text-transform: capitalize;
    }
  }
}
</style>
