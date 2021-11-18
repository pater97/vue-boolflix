<template>
  <div>
    <section class="search_bar">
      <input v-model="searchText" type="text" />
      <button class="search_btn"  @click="getCall">search</button>
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      searchText: "",
      callApi:
        "https://api.themoviedb.org/3/search/movie?api_key=f4f382566368553eb6b723d584f2ef40&language=en-US&query=" + this.searchText,
      moviesArray: "",
    };
  },
  methods: {
    getCall() {
      axios
        .get(this.callApi)
        .then((response) => {
          console.log(response);
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