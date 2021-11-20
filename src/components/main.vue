<template>
  <div class="container_main">
    <!-- container film  -->
    <section class="show_films">
      <div class="films" v-for="film in movies" :key="film.id">
        <cards :film="film" />
      </div>
    </section>
    <!-- / container film  -->
  </div>
</template>

<script>
import cards from "./cards.vue";
export default {
  components: {
    cards,
  },
  props: {
    movies: Array,
  },
};
</script>

<style lang="scss">
.show_films{
  display: flex;
  flex-wrap: wrap;
  width: 97%;
  margin: auto;
  .films{
    width: calc(100%/5);
    margin: 2rem 0;
  }
}
</style>