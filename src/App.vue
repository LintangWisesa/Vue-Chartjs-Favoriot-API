<template>
  <div>
    <button v-on:click="get">Klik</button>
    <ul>
      <li v-for="(x, i) in dataout" :key="i">
        {{ x.id }} {{ x.title }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return {
      dataout: []
    }
  },
  methods: {
    get(){
      axios.get('https://jsonplaceholder.typicode.com/posts')
      .then((x)=>{
        console.log(x.data)
        this.dataout = x.data
      })
    }
  }
}
</script>

<style>
</style>
