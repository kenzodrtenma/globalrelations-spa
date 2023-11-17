<template>
  <div class="homepage">
    <h1>globalrelations.com</h1>
    <p>Select two countries and get their “relationship status”.</p>
    <CountriesSelector></CountriesSelector>
  </div>
</template>

<script>

import CountriesSelector from './CountriesSelector.vue'

export default {
  name: 'HomePage',
  components: {
    CountriesSelector
  },
  props: {
    msg: String
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
    margin-bottom: 100px;
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
