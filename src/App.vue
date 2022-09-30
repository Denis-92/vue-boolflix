<template>
  <div id="app">
    <h1>TEST TEST</h1>
  </div>
</template>


<script>
import axios from 'axios';
import { keyAPI } from '@/env.js'

export default {
  name: 'App',
  created() {
    this.queryAPI();
  },
  methods: {
    queryAPI() {
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${keyAPI}&query=ritorno+al+futuro`).then(
        (response) => {
          console.log('response= ', response);
        }
      ).catch(
        error => {
          console.log('error= ', error.message);
        }
      )
    }
  }
}
</script>


<style lang="scss">

</style>
