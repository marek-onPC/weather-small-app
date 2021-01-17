<template>
  <div class="mdl-card">
    <div class="mdl-textfield mdl-js-textfield">
      <input class="mdl-textfield__input" type="text" id="search_city" v-model="searchCity" v-on:keyup="searchNameInputed">
      <label class="mdl-textfield__label" for="search_city">City...</label>
    </div>
  </div>
</template>

<script>
import debounce from 'lodash.debounce'

export default {
  name: 'Search',
  data () {
    return {
      searchCity: ''
    }
  },
  methods: {
    searchNameInputed:
      debounce(function () {
        console.log(this.searchCity)
        this.$emit('search-city', this.searchCity)
      }, 500)
  }
}
</script>

<style lang="scss" scoped>
.mdl-card {
  align-items: center;
  min-height: 0;
  color: #222;
  margin: auto;
}
</style>
