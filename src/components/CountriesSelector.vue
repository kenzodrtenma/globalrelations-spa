<template>
    <div class="world-loading" v-if="loading">
      <div class="world-loading-image">
        <img src="../assets/world-loading.gif" alt="image of a earth globe spinning">
      </div>
      <span>Carregando países...</span>
    </div>
    <div  v-if="!loading && data" class="countries-selector">
      <div class="selectors">
        <div class="selector">
          <div class="flag">
            <div v-if="first_flag_loading" class="world-loading-image">
              <img src="../assets/world-loading.gif" alt="image of a earth globe spinning">
            </div>
            <img v-if="!first_flag_loading" :src="first_country_flag" alt="">
          </div>
          <select v-model="first_country" @change="handleCountrySelect(1)">
            <option value="default">Select the first country</option>
            <option v-for="country in countries" :key="country.name" :value="country.name">
              {{ country.name.common }}
            </option>
          </select>
        </div>
        <p>and</p>
        <div class="selector">
          <div class="flag">
            <div v-if="second_flag_loading" class="world-loading-image">
              <img src="../assets/world-loading.gif" alt="image of a earth globe spinning">
            </div>
            <img v-if="!second_flag_loading" :src="second_country_flag" alt="">
          </div>
          <select v-model="second_country" @change="handleCountrySelect(2)">
            <option value="default">Select the second country</option>
            <option v-for="country in countries" :key="country.name" :value="country.name">              
              {{ country.name.common }}
            </option>
          </select>
        </div>
      </div>
      <button class="submit">Check</button>
    </div>
</template>
  
<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        data: [],
        countries: [],
        first_country: "default",
        second_country: "default",
        first_country_flag: require("../assets/un.png"),
        second_country_flag: require("../assets/un.png"),
        first_flag_loading: false,
        second_flag_loading: false,
        loading: true
      };
    },

    methods: {
      getCountries() {
        this.loading = true;

        axios.get('https://restcountries.com/v3.1/independent?status=true')
        .then(response => {
          this.loading = false
          this.countries = response.data
          this.countries = this.orderByNameASC(response.data)
        })
        .catch(error => {
          console.error("Erro na requisição:", error)
          this.loading = false
        })
      },

      handleCountrySelect(country_number) {        
        if (country_number == 1 && this.first_country != 'default') {
          this.first_flag_loading = true;
          let selected_country = this.countries.find(country => country.name == this.first_country)
          this.first_country_flag = selected_country.flags.svg

          setTimeout(() => {
            this.first_flag_loading = false
          }, 500);
          
        } else if (country_number == 2 && this.second_country != 'default') {
          this.second_flag_loading = true;
          let selected_country = this.countries.find(country => country.name == this.second_country)
          this.second_country_flag = selected_country.flags.svg

          setTimeout(() => {
            this.second_flag_loading = false
          }, 500);
        }

        if (this.first_country == 'default') {
          this.first_country_flag = require('../assets/un.png')
        }

        if (this.second_country == 'default') {
          this.second_country_flag = require('../assets/un.png')
        }
      },

      orderByNameASC(countries) {
        return countries.sort((a, b) => {
          const nameA = a.name.common.toUpperCase();
          const nameB = b.name.common.toUpperCase();

          if (nameA < nameB) {
            return -1
          }

          if (nameA > nameB) {
            return 1
          }

          return 0
        })
      }
    },

    created() {
      this.getCountries()
    }
  };
</script>

<style>

  .world-loading {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .world-loading-image {
    width: 150px;
    height: 150px;
    margin-bottom: 10px;
  }

  .world-loading-image img {
    width: 100%;
    height: 100%;
  }

  .countries-selector .selectors {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    width: 100%;
  }

  .countries-selector .selector,
  .countries-selector select {
    width: 100%;
  }

  .countries-selector select option {
    height: 10px;
  }

  .countries-selector select,
  .countries-selector .submit {
    height: 50px;
    font-size: 20px;
  }

  .countries-selector p {
    margin: 15px 0;
    font-size: 30px;
  }

  .countries-selector .flag {
    display: none;
  }

  .countries-selector .flag img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .countries-selector .submit {
    width: 100%;
    margin-top: 30px;
    background: #15A24A;
    color: #fff;
    border: 2px solid #15A24A;
  }

  .countries-selector .submit:hover {
    background: #fff;
    color: #15A24A;
  }  


  @media screen and (min-width: 768px) {
    .countries-selector .flag {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 320px;
      height: 220px;
      margin-bottom: 30px;
      border: 2px solid #999;
      border-radius: 10px;
      overflow: hidden;
    }

    .countries-selector .selector,
    .countries-selector select,
    .countries-selector .submit {
      width: 320px;
    }

    .countries-selector .submit {
      margin-top: 100px;
    }

    .countries-selector p {
      margin: 0 30px;
    }
  }

</style>