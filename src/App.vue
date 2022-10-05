<template>
  <div id="app">

    <div id="header">
      <h1>BOOLFLIX</h1>
      <div>
        <input type="text" v-model="search">
        <button @click="filter">Search</button>
      </div>
    </div>

    <div id="content-box">
      <div>
        <componentCardsVue v-for="movie in content" :key="movie.id" class="single-content" :title="movie.title"
          :original-title="movie.original_title" :language="movie.original_language" :vote="movie.vote_average"
          :image="movie.poster_path" />
      </div>
      <div>
        <componentCardsVue v-for="series in seriesTv" :key="series.id" class="single-content" :title="series.name"
          :original-title="series.original_name" :language="series.original_language" :vote="series.vote_average"
          :image="series.poster_path" />
      </div>
    </div>
  </div>
</template>


<script>
import axios from 'axios';
import { keyAPI } from '@/env.js';
import componentCardsVue from '@/components/componentCards.vue';

export default {
  name: 'App',
  components: {
    componentCardsVue,
  },
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
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#header {
  background-color: black;
  color: white;
  height: 10vh;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}

#content-box {
  height: 90vh;
  background-color: grey;
  color: white;
  display: flex;
  justify-content: center;

  >div {
    margin: 1%;
    height: 90%;
    display: flex;
    overflow-x: auto;
  }
}

.single-content {
  margin: 1%;
  border: 1px solid white;
}
</style>
