<template>
  <div>
    <SearchBar placeholder="Cosa Guardiamo oggi?" @search="startSearch"/>

    <!-- sezione movies -->
    <section id="movies">
      <h2>Movies</h2>
      <ul v-for="movie in movies" :key="movie.id">
        <li>{{movie.title}}</li>
        <li>{{movie.original_title}}</li>
        <li>{{movie.original_language}}</li>
        <li>{{movie.vote_average}}</li>
      </ul>
    </section>

        <!-- sezione series -->
    <section id="movies">
      <h2>Series</h2>
      <ul v-for="serie in series" :key="serie.id">
        <li>{{serie.name}}</li>
        <li>{{serie.original_name}}</li>
        <li>{{serie.original_language}}</li>
        <li>{{serie.vote_average}}</li>
      </ul>
    </section>
  </div>
</template>

<script>

import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
export default {
  name: 'App',
  components: {
    SearchBar
  },
  data(){
    return{
      movies:[],
      series:[],
      api:{
        language: 'it-IT',
        key:'fc33cd5a7fe520146f021c17216ee8d6',
        baseUri:'https://api.themoviedb.org/3',
      }

    }
  },
  methods:{
    startSearch(query){
      if(!query){
        this.movies = this.series = [];
        return;
      }
      // chiamata Api
      const {language, key} = this.api;

      const config = {
        params:{
          api_key : key,
          language,
          query,
        }
      };

      this.fetchData('/search/movie',config, 'movies');
      this.fetchData('/search/tv',config, 'series');
    },

    fetchData(endpoint,config,target){
      axios.get(`${this.api.baseUri}${endpoint}`, config).then((res)=>{
        // gestione risposta
        this[target] = res.data.results;
      });
    }
  }

}
</script>

<style lang="scss">
</style>


