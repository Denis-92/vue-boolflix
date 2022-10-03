<template>
  <div id="app">
    <h1>TEST TEST</h1>
    <input type="text" v-model="search">
    <button @click="filter">Search</button>

    <div id="content-box">
      <div v-for="movie in content" :key="movie.id" class="single-content">
        <p> TITOLO: {{ movie.title }} </p>
        <p> TITOLO ORIGINALE: {{ movie.original_title }} </p>
        <p> LINGUA ORIGINALE: <img :src="showIcon(movie.original_language)" alt="Flag icon" class="icon-flag">{{
        movie.original_language }} </p>
        <p> VOTO: {{ movie.vote_average }} </p>
      </div>
    </div>
  </div>
</template>


<script>
import axios from 'axios';
import { keyAPI } from '@/env.js';

export default {
  name: 'App',
  data() {
    return {
      search: '',
      content: [],
    };
  },
  methods: {
    showIcon(language) {
      return `https://flagicons.lipis.dev/flags/1x1/${language}.svg`;
    },
    filter() {
      this.queryAPI(this.search);
      this.search = ''; //reset della textbox a fine ricerca
    },
    queryAPI(inputFilter) {
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${keyAPI}&query=${inputFilter}&language=it-IT`).then(
        (response) => {
          console.log('response= ', response);
          if (response.status === 200) {
            this.content = response.data.results;
            console.log('array contenuto', this.content);
          }
        }
      ).catch(
        error => {
          console.log('error= ', error.message);
        }
      );
    },
  },
}
</script>


<style lang="scss">
#content-box {
  background-color: goldenrod;
  color: white;
  margin: 0 auto;
  max-width: 1000px;
  margin-top: 2%;
}

.single-content {
  border: 1px solid black;
}

.icon-flag {
  max-width: 12px;
}
</style>
