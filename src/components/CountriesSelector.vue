<template>
    <div class="countries-selector">
      <div class="selectors">
        <div class="selector">
          <div class="flag">
            <img src="https://flagcdn.com/br.svg" alt="">
          </div>
          <select>
            <option v-for="country in countries" :key="country.name" :value="country.name">
              {{ country.name }}
            </option>
          </select>
        </div>
        <p>and</p>
        <div class="selector">
          <div class="flag">
            <img src="https://flagcdn.com/br.svg" alt="">
          </div>
          <select>
            <option v-for="country in countries" :key="country.name" :value="country.name">
              {{ country.name }}
            </option>
          </select>
        </div>
      </div>
      <button class="submit">Check</button>
    </div>
</template>
  
<script>
  export default {
    data() {
      return {
        countries: []
      };
    },

    methods: {
      getCountries() {
        this.countries = [
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'},
          {'name': 'Brazil'}
        ]
      }
    },

    created() {
      this.getCountries()
    }
  };
</script>

<style>

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
    width: 320px;
    height: 220px;
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
      display: block;
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