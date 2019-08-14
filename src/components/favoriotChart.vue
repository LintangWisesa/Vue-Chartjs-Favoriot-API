<template>
  <div class="small">
    
    <form class="col s12">
      <div class="row">
        
        <div class="input-field col s3">
          <input id="temp" type="text" class="validate" ref='temp'>
          <label for="temp">Temperature...</label>
        </div>

        <div class="input-field col s3">
          <input id="hum" type="text" class="validate" ref='hum'>
          <label for="hum">Humidity...</label>
        </div>

        <div class="input-field col s3">
          <input id="pot" type="text" class="validate" ref='pot'>
          <label for="pot">Potentiometer...</label>
        </div>

        <div class='col s3'>
          <div class="row">
            <a class="col s6 waves-effect waves-light btn-large teal lighten-2"
            @click="getFavoriot()"
            >
              <i class="material-icons">cloud_download</i>
            </a>

            <a class="col s6 waves-effect waves-light btn-large pink lighten-1"
            @click="postFavoriot()"
            >
              <i class="material-icons">cloud_upload</i>
            </a>
          </div>
        </div>

      </div>
    </form>

    <line-chart 
      v-if="loaded" 
      :chart-data="datacollection"
    ></line-chart>
  
  </div>
</template>

<script>
  import LineChart from './favoriotLine.js'
  import axios from 'axios'
  // npm i axios

  export default {
    components: {
      LineChart
    },
    data () {
      return {
        datacollection: null,
        loaded: false,
        temperature: [0,1,2,3,4,5,6,7,8,9],
        humidity: [9,8,7,6,5,4,3,2,1,0],
        potentio: [4,5,4,5,4,5,4,5,4,5],
        time: [0,1,2,3,4,5,6,7,8,9]
      }
    },
    async mounted () {
      this.fillData()
      this.loaded = false
      await this.getFavoriot()
    },
    methods: {
      fillData () {
        this.datacollection = {
          labels: this.time,
          datasets: [
            {
              label: 'Temp (°C)',
              backgroundColor: 'rgba(0, 0, 255, 0.2)',
              borderColor: 'lightblue', 
              pointBackgroundColor: 'blue', 
              borderWidth: 1, 
              pointBorderColor: 'blue',
              // data: [1,2,3,2,1,3,4,6,7,8]
              data: this.temperature
            }, 
            {
              label: 'Hum (%)',
              backgroundColor: 'rgba(255, 0, 0, 0.2)',
              borderColor: 'lightpink', 
              pointBackgroundColor: 'red', 
              borderWidth: 1, 
              pointBorderColor: 'red',
              // data: [6,7,6,8,7,8,6,7,6,6]
              data: this.humidity
            },
            {
              label: 'Potentio',
              backgroundColor: 'rgba(255, 255, 0, 0.2)',
              borderColor: 'yellow', 
              pointBackgroundColor: 'orange', 
              borderWidth: 1, 
              pointBorderColor: 'orange',
              // data: [6,7,6,8,7,8,6,7,6,6]
              data: this.potentio
            }
          ]
        }
      },
      tesInput(){
        alert(this.$refs.temp.value + this.$refs.hum.value + this.$refs.pot.value)
      },
      getRandomInt () {
        return Math.floor(Math.random() * (50 - 5 + 1)) + 5
      },
      tesGet(){
        this.temperature = [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()]
        this.humidity = [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()]
        this.fillData()
      },
      getFavoriot(){
        var url = 'https://api.favoriot.com/v1/streams?device_developer_id=deviceDefault@Lintang_Wisesa&max=10'
        var headers = {
          headers: {
            'Content-Type': 'application/json',
            'apikey': 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IkxpbnRhbmdfV2lzZXNhIiwicmVhZF93cml0ZSI6dHJ1ZSwiaWF0IjoxNDkzODgyODczfQ.0n_FIr4vapSjewJE2e7cb-FTXs3JsUMTHsTgT2mYNFs'
          }
        }
        axios.get(url, headers)
        .then((x)=>{
          var results = x.data.results
          var temp = []
          var hum = []
          var pot = []
          var time = []
          for(var i=9; i>=0; i--){
            var t = parseInt(results[i].data.Temperature)
            var h = parseInt(results[i].data.Humidity)
            var p = parseInt(results[i].data.Potentio)
            var ti = results[i].stream_created_at.split('T')
            
            temp.push(t)
            hum.push(h)
            pot.push(p)
            time.push(ti)
          }
          // console.log(results)
          // console.log(temp)
          // console.log(hum)
          // console.log(pot)
          this.temperature = temp
          this.humidity = hum
          this.potentio = pot
          this.time = time
          this.loaded = true
          this.fillData()
        })
        .catch(()=>{
          alert('Failed to get the data 😭')
        })
      },
      postFavoriot(){
        var url = 'https://api.favoriot.com/v1/streams'
        var headers = {
          headers: {
            'Content-Type': 'application/json',
            'apikey': 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IkxpbnRhbmdfV2lzZXNhIiwicmVhZF93cml0ZSI6dHJ1ZSwiaWF0IjoxNDkzODgyODczfQ.0n_FIr4vapSjewJE2e7cb-FTXs3JsUMTHsTgT2mYNFs'
          }
        }
        var dataBody = {
          device_developer_id: "deviceDefault@Lintang_Wisesa",
          data: {
            Temperature: this.$refs.temp.value,
            Humidity: this.$refs.hum.value,
            Potentio: this.$refs.pot.value,
          }
        }
        axios.post(url, dataBody, headers)
        .then(()=>{
          alert('Data posted successfully! 😍')
          this.getFavoriot()
        })
        .catch(()=>{
          alert('Failed to post the data 😭')
        })
      }
    }
  }
</script>

<style>
  .small {
    width: 500px;
    height: 100px;
    margin: auto
  }
</style>