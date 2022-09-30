<template>
  <div id="app">
    <h1>TEST TEST</h1>
    <input type="text" v-model="search">
    <button @click="filter">Search</button>
  </div>
</template>


<script>
import axios from 'axios';
import { keyAPI } from '@/env.js'

export default {
  name: 'App',
  data() {
    return {
      search: ''
    }
  },
  methods: {
    filter() {
      this.queryAPI(this.search);
    },
    queryAPI(inputFilter) {
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${keyAPI}&query=${inputFilter}&language=it-IT`).then(
        (response) => {
          console.log('response= ', response);
        }
      ).catch(
        error => {
          console.log('error= ', error.message);
        }
      )
    },
  }
}
</script>


<style lang="scss">

</style>
