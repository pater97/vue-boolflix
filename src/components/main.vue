<template>
  <div>
    <!-- sezione barra di ricerca   -->
    <section class="search_bar">
      <input v-model="searchText" type="text" />
      <button class="search_btn" @click="getCall">search</button>
    </section>
    <!-- /sezione barra di ricerca   -->
    <!-- container film  -->
    <section class="show_films">
      <div class="films" v-for="film in moviesArray" :key="film.id">
        <h1>titolo:{{ film.title }}</h1>
        <h2>titolo originale: {{ film.original_title }}</h2>
        <h5>lenguage: {{ film.original_language}}</h5>
        <h3>vote: {{ film.vote_average }}</h3>
        <hr />
      </div>
    </section>
    <!-- / container film  -->
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      searchText: "",
      moviesArray: [],
    };
  },
  methods: {
    // funzione che richiama l'api al click del bottone   
    getCall() {
      axios
        .get(
          "https://api.themoviedb.org/3/search/movie?api_key=f4f382566368553eb6b723d584f2ef40&query=" +
            this.searchText
        )
        .then((response) => {
          this.moviesArray = response.data.results;
          console.log(this.moviesArray);
        })
        .catch((e) => {
          console.log(e, "ops!");
        });
    },
  },
};
</script>

<style lang="scss">
</style>