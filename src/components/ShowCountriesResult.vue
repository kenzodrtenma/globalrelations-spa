<template>
    <div class="world-loading">
      <div class="world-loading-image">
        <img src="../assets/world-loading.gif" alt="image of a earth globe spinning">
      </div>
      <span>Analisando relacionamento entre {{ selectedCountries[0][0] }} e {{ selectedCountries[0][1] }}...</span>
    </div>
</template>
  
<script>
  export default {
    props: {
      selectedCountries: {
        type: Array,
        required: true,
      },
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