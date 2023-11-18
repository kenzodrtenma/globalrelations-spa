<template>
  <HomePage></HomePage>
</template>

<script>
import HomePage from './components/HomePage.vue'

export default {
  name: 'App',
  components: {
    HomePage
  }
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
}

body {
  min-height: 100vh;
  background-color: #f4f4f4;
}

#app {
  font-family: 'Inter', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  padding-bottom: 30px;
  padding-left: 20px;
  padding-right: 20px;
}

@media screen and (min-width: 768px) {
  #app {
    padding-left: 0;
    padding-right: 0;
  }
}
</style>
