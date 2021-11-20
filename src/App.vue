<template>
  <div id="app">
    <!-- header -->
    <siteHeader @getCall="getCall" />
    <!-- main -->
    <siteMain :movies="movies" />
  </div>
</template>

<script>
// importazioni
import siteHeader from "./components/header.vue";
import siteMain from "./components/main.vue";
import axios from "axios";
import "@fontsource/bebas-neue";

export default {
  name: "App",
  components: {
    siteMain,
    siteHeader,
  },
  data() {
    return {
      searchString: "",
      movies: [],
      apiKey: "f4f382566368553eb6b723d584f2ef40&query=",
      apiFilm: "https://api.themoviedb.org/3/search/movie?api_key=",
      apiSeries: "https://api.themoviedb.org/3/search/tv?api_key=",
    };
  },
  methods: {
    // funzione per mostrare le chiamate insieme
    getCall(searchText) {
      this.searchString = searchText;
      this.getSeries(this.apiSeries);
      this.getMovies(this.apiFilm);
    },
    // popolare l'array con la chiamata apy 
    getSeries(api) {
      axios
        .get(api + this.apiKey + this.searchString)
        .then((response) => {
          this.movies = response.data.results;
        })
        .catch((e) => {
          console.log(e, "ops!");
        });
    },
    // aggiungere tramite un push le serie tv
    getMovies(api) {
      axios
        .get(api + this.apiKey + this.searchString)
        .then((response) => {
          const singleObject = response.data.results;
          for (let i = 0; i < singleObject.length; i++) {
            this.movies.push(singleObject[i]);
          }
          console.log(this.movies);
        })
        .catch((e) => {
          console.log(e, "ops!");
        });
    },
  },
};
</script>

<style lang="scss">
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Bebas Neue";
  background-color: #141414;
}
</style>
