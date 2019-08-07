<template>
  <div id="app">
    <h3>Favoriot ♥ Vue ♥ Vue-Chart.js</h3>
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
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
</style>
