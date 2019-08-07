<template>
  <div id="app">
    <h1>Favoriot ♥ Vue ♥ Vue-Chart.js</h1>
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <FavoriotChart/>
    <!-- <tesChart/>     -->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import FavoriotChart from './components/favoriotChart.vue'
// import tesChart from './components/vueChart_tes.vue'

export default {
  name: 'app',
  components: {
    FavoriotChart
    // tesChart
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
</style>
