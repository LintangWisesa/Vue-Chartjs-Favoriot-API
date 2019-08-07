<template>
  <div class="small">
    <Chart :chart-data="datacollection"></Chart>
    <button @click="tesGet()">Randomize</button>
  </div>
</template>

<script>
  import Chart from './vueChart_line.js'
  // import Chart from './vueChart_bar.js'
  
  export default {
    components: {
      Chart
    },
    data () {
      return {
        datacollection: null,
        data1: [0,1,2,3,4,5,6,7,8,9],
        data2: [9,8,7,6,5,4,3,2,1,0],
        data3: [4,5,4,5,4,5,4,5,4,5],
      }
    },
    mounted () {
      this.fillData()
    },
    methods: {
      fillData () {
        this.datacollection = {
          labels: [0,1,2,3,4,5,6,7,8,9],
          datasets: [
            {
              label: 'Data One',
              backgroundColor: 'rgba(0, 0, 255, 0.2)',
              borderColor: 'lightblue', 
              pointBackgroundColor: 'blue', 
              borderWidth: 1, 
              pointBorderColor: 'blue',
              // data: [1,2,3,2,1,3,4,6,7,8]
              data: this.data1
            }, 
            {
              label: 'Data Two',
              backgroundColor: 'rgba(255, 0, 0, 0.2)',
              borderColor: 'lightpink', 
              pointBackgroundColor: 'red', 
              borderWidth: 1, 
              pointBorderColor: 'red',
              // data: [6,7,6,8,7,8,6,7,6,6]
              data: this.data2
            },
            {
              label: 'Data Three',
              backgroundColor: 'rgba(255, 255, 0, 0.2)',
              borderColor: 'yellow', 
              pointBackgroundColor: 'orange', 
              borderWidth: 1, 
              pointBorderColor: 'orange',
              // data: [6,7,6,8,7,8,6,7,6,6]
              data: this.data3
            }
          ]
        }
      },
      getRandomInt () {
        return Math.floor(Math.random() * (50 - 5 + 1)) + 5
      },
      tesGet(){
        this.data1 = [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()]
        this.data2 = [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()]
        this.data3 = [35,40,35,40,35,40,35,40,35,40]
        this.fillData()
      },
    }
  }
</script>

<style>
  .small {
    width: 400px;
    height: 100px;
    margin: 150px auto;
  }
</style>