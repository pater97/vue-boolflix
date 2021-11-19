<template>
  <div>
    <!-- container film  -->
    <section class="show_films">
      <div class="films" v-for="film in movies" :key="film.id">
        <cards :film="film" />
        <!-- barra temporanea per marcare la divisione  -->
        <hr />
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
.vote {
  img {
    width: 15px;
  }
}
</style>