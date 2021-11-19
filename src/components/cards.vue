<template>
  <div class="card">
    <!-- copertina card  -->
    <div class="cover">
      <!-- se trovata -->
      <img
        v-if="film.poster_path"
        :src="coverLink + film.poster_path"
        :alt="film.title"
      />
      <!-- immagine non trovata  -->
      <img
        v-else
        src="https://bitsofco.de/content/images/2018/12/broken-1.png"
        :alt="film.title"
      />
    </div>
    <!-- titolo -->
    <div class="title">
      <h1 v-if="film.title">titolo:{{ film.title }}</h1>
      <h1 v-else>titolo: {{ film.name }}</h1>
    </div>
    <!-- titolo originale -->
    <div class="original_title">
      <h2 v-if="film.original_title">
        titolo originale: {{ film.original_title }}
      </h2>
      <h2 v-else>titolo originale: {{ film.original_name }}</h2>
    </div>
    <!-- voto -->
    <span
      class="vote"
      v-for="finalVote in Math.round(film.vote_average / 2)"
      :key="finalVote"
    >
      <img src="../assets/star-solid.svg" alt="" />
    </span>
    <!-- sezione flag e language -->
    <div class="lenguage">
      <h5>lenguage: {{ film.original_language }}</h5>
      <!-- bandiere frequenti da convertire -->
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
      <!-- bandiere presenti nella libreria -->
      <country-flag v-else :country="film.original_language" size="normal" />
    </div>
  </div>
</template>

<script>
import CountryFlag from "vue-country-flag";
export default {
  components: {
    CountryFlag,
  },
  props: {
    film: Object,
  },
  data() {
    return {
      coverLink: "http://image.tmdb.org/t/p/w342/",
    };
  },
};
</script>