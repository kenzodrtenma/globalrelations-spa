<template>
  <div class="homepage">
    <h1>globalrelations.com</h1>
    <p>Select two countries and get their “relationship status”.</p>
    <CountriesSelector v-if="!showCountriesResult" @user-selected-countries="countriesSelected"></CountriesSelector>
    <ShowCountriesResult v-if="showCountriesResult" :selectedCountries="selectedCountries"></ShowCountriesResult>
  </div>
</template>

<script>

import CountriesSelector from './CountriesSelector.vue'
import ShowCountriesResult from './ShowCountriesResult.vue'


export default {
  name: 'HomePage',
  data() {
    return {
      selectedCountries: [],
      showCountriesResult: false
    }
  },
  components: {
    CountriesSelector,
    ShowCountriesResult
  },
  props: {
    msg: String
  },
  methods: {
    countriesSelected(selected_countries) {
      this.selectedCountries = selected_countries
      this.showCountriesResult = true
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .homepage h1,
  .homepage p {
    color: #000000;
  }
  .homepage h1 {
    font-weight: bold;
    font-size: 27px;
    margin-bottom: 20px;
  }

  .homepage p {
    font-size: 17px;
    margin-bottom: 30px;
  }

  /* Ipad Pro, Desktop */
  @media screen and (min-width: 768px) {
    .homepage h1 {
      font-size: 50px;
    }
    .homepage p {
      font-size: 20px;
    }
  }

  /* Micro-dispositivos */
  @media screen and (max-width: 312px) {
    .homepage h1 {
      font-size: 20px;
    }
    .homepage p {
      font-size: 15px;
    }
  }
</style>
