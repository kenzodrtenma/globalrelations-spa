<template>
    <div class="show-countries-relation">
      <div v-if="loading" class="world-loading">
        <div class="world-loading-image">
          <img src="../assets/world-loading.gif" alt="image of a earth globe spinning">
        </div>
        <span>Analisando relacionamento entre {{ first_country.name.common }} e {{ second_country.name.common }}...</span>
      </div>

      <div v-if="!loading" class="content">
        <div class="countries-images">
          <div class="container">
            <img :src="first_country.flags.svg" alt="">
          </div>
          <div class="container">
            <img :src="second_country.flags.svg" alt="">
          </div>
        </div>
        <section class="relationship-status">
          <h2>Relationship status:</h2>
          <p :style="relationship_color">{{ relationship.relationship_status }}</p>
        </section>
        <section class="few-words">
          <h2>Well boy, in a few words...</h2>
          <p>{{ relationship.in_a_few_words }}</p>
        </section>
      </div>

    </div>
</template>
  
<script>
  import axios from 'axios';

  export default {
    props: {
      selectedCountries: {
        type: Array,
        required: true
      }
    },

    data() {
      return {
        apiUrl: process.env.VUE_APP_FLASK_API_URL,
        loading: true,
        relationship: [],
        relationship_color: "",
        first_country: this.selectedCountries[0][0],
        second_country: this.selectedCountries[0][1]
      }
    },

    methods: {
      getCountriesRelationshipInfo() {
        const countries_relation_url = this.apiUrl 
          + '?first_country=' + this.first_country.name.common 
          + '&second_country=' + this.second_country.name.common

        axios.get(countries_relation_url)
        .then(response => {
          console.log(this.first_country)
          console.log(response.data)
          this.relationship = response.data
          this.relationship_color = "color: " + this.relationship.relationship_color
          this.loading = false
        })
        .catch(error => {
          console.error("Erro na requisição:", error)
          this.loading = false
        })
      }
    },

    mounted() {
      this.getCountriesRelationshipInfo()
    }
  };
</script>

<style>

  .show-countries-relation {
    padding: 20px;
  }
  .show-countries-relation .countries-images{
      display: flex;
      justify-content: center;
      align-items: center;
      margin-bottom: 30px;
  }

  .show-countries-relation .countries-images .container{
    display: flex;
    height: 100px;
    border: 2px solid #999;
    border-radius: 10px;
    overflow: hidden;
    width: 12em;
    height: 6.5em;
  }

  .show-countries-relation .countries-images .container:first-child{
    margin-right: 30px;
  }

  .show-countries-relation .countries-images .container img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  section.relationship-status h2 {
    font-size: 18px;
    font-weight: 400;
    margin-bottom: 10px;
    text-transform: uppercase;
    font-style: italic;
  }

  section.relationship-status p {
    font-weight: bolder;
    font-size: 2em;
  }

  .show-countries-relation section {
    margin-bottom: 50px;
  }

  .show-countries-relation section:last-child {
    margin-bottom: 0px;
  }

  .show-countries-relation section.few-words {
    text-align: left;
  }

  .show-countries-relation section.few-words h2 {
    font-size: 2em;
    margin-bottom: 15px;
  }

  .show-countries-relation section.few-words p {
    font-size: 1.5em;
    margin-bottom: 15px;
  }

  @media screen and (min-width: 768px) {
    .show-countries-relation .countries-images .container {
      width: 180px;
      height: 110px;
    }
  }

  /* Micro-dispositivos */
  @media screen and (max-width: 312px) {
    .show-countries-relation .countries-images .container {
      height: 5em;
    }
  }

</style>