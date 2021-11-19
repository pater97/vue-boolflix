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
      <div class="films" v-for="film in movies" :key="film.id">
        <!-- copertina -->
        <div class="cover">
          <img v-if="film.poster_path" :src="coverLink + film.poster_path" alt="">
          <img v-else src="https://bitsofco.de/content/images/2018/12/broken-1.png" alt="">
        </div>
        <!-- titolo -->
        <div class="title">
          <h1 v-if="film.title">titolo:{{ film.title }}</h1>
          <h1 v-else>titolo: {{ film.name }}</h1>
        </div>
        <!-- /tiotolo -->
        <!-- titolo originale -->
        <div class="original_title">
          <h2 v-if="film.original_title">
            titolo originale: {{ film.original_title }}
          </h2>
          <h2 v-else>titolo originale: {{ film.original_name }}</h2>
        </div>
        <!-- /titolo originale -->
        <!-- voto -->
        <div class="vote">
          <h3>vote: {{ film.vote_average }}</h3>
        </div>
        <!-- /voto -->
        <!-- sezione flag e language -->
        <div class="lenguage">
          <h5>lenguage: {{ film.original_language }}</h5>
          <country-flag
            v-if="film.original_language == 'en'"
            country="gb"
            size="normal"
          />
          <country-flag
            v-else-if="film.original_language == 'ja'"
            country="jp"
            size="normal"
          />
          <country-flag
            v-else
            :country="film.original_language"
            size="normal"
          />
        </div>
        <!-- /sezione flag e language -->
        <hr />
      </div>
    </section>
    <!-- / container film  -->
  </div>
</template>

<script>
import axios from "axios";
import CountryFlag from "vue-country-flag";
export default {
  components: {
    CountryFlag,
  },
  data() {
    return {
      searchText: "",
      apiKey:'f4f382566368553eb6b723d584f2ef40&query=',
      apiFilm:'https://api.themoviedb.org/3/search/movie?api_key=',
      apiSeries:'https://api.themoviedb.org/3/search/tv?api_key=',
      movies: [],
      coverLink: 'http://image.tmdb.org/t/p/w500/',
    };
  },
  methods: {
    // funzione che richiama l'api al click del bottone sia serie tv che film.
    getCall(){
      this.getSeries(this.apiSeries)
      this.getMovies(this.apiFilm)
    },
     getMovies(api) {
      axios
        .get(
          api + this.apiKey + this.searchText
        )
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
     getSeries(api) {
      axios
        .get(
          api + this.apiKey + this.searchText
        )
        .then((response) => {
          this.movies = response.data.results;
        })
        .catch((e) => {
          console.log(e, "ops!");
        });
    }
  },
};
</script>

<style lang="scss">
</style>