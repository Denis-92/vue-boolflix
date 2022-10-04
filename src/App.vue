<template>
  <div id="app">
    <h1>TEST TEST</h1>
    <input type="text" v-model="search">
    <button @click="filter">Search</button>

    <div id="content-box">
      <div v-for="movie in content" :key="movie.id" class="single-content">
        <p> TITOLO: {{ movie.title }} </p>
        <p> TITOLO ORIGINALE: {{ movie.original_title }} </p>
        <p>
          LINGUA ORIGINALE: <img :src="showIcon(movie.original_language)" :alt="movie.original_language"
            class="icon-flag" @error="detectErrorFlag($event)">
        </p>
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
      seriesTv: [],
    };
  },
  methods: {
    showIcon(language) {
      language = this.convertLanguageCode(language);
      return `https://flagicons.lipis.dev/flags/1x1/${language}.svg`;
    },
    convertLanguageCode(language) {
      switch (language) {
        case 'ja': {
          language = 'jp';
          break;
        }
        case 'en': {
          language = 'gb';
          break;
        }
      }
      return language;
    },
    detectErrorFlag(event) {
      event.target.src = `https://flagicons.lipis.dev/flags/1x1/xx.svg`;
    },
    filter() {
      this.queryAPI(this.search);
      this.search = ''; //reset della textbox a fine ricerca
    },
    queryAPI(inputFilter) {
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${keyAPI}&query=${inputFilter}&language=it-IT`).then(
        (response) => {
          this.content = this.makeResponseAPI(response);
        }
      ).catch(
        error => {
          console.log('error= ', error.message);
        }
      );
      axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${keyAPI}&query=${inputFilter}&language=it-IT`).then(
        (response) => {
          this.seriesTv = this.makeResponseAPI(response);
        }
      ).catch(
        error => {
          console.log('error= ', error.message);
        }
      );
    },
    makeResponseAPI(response) {
      console.log('response= ', response);
      if (response.status === 200) {
        return response.data.results;
      } else {
        return [];
      }
    }
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
