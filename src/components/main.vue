<template>
  <div class="container_main">
    <!-- container film  -->
    <section class="show_films" v-if="ifEmpty()">
      <div class="films" v-for="film in movies" :key="film.id" >
        <cards :film="film"/>
      </div>
    </section>
    <section class="search_films" v-else>
      <h1>Cerca un film o una serie tv...</h1>
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
  methods:{
    ifEmpty(){
      if(this.movies.length !== 0){
        return true
      }else{
        return false
      }
    }
  }
};
</script>

<style lang="scss">
.show_films , .search_films{
  display: flex;
  flex-wrap: wrap;
  width: 97%;
  margin: auto;
  .films{
    width: calc(100%/5);
    margin: 2rem 0;
  }
}
.search_films{
  height: 30rem;
  justify-content: center;
  align-items: center;
  color: #e50914;
  font-size: 2.5rem;
  
  
}
</style>