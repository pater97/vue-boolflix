<template>
  <div class="container_header">
      <!-- logo  -->
    <div class="logo">
      <h1>BOOLFLIX</h1>
    </div>
    <!-- sezione barra di ricerca   -->
    <section class="search_bar">
      <input
        v-model="searchText"
        type="text"
        placeholder="Search"
        @keyup.enter="$emit('getCall', searchText)"
      />
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchText: "",
    };
  },
};
</script>

<style lang="scss">
.container_header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 95%;
    margin: 1rem auto;
}
.logo {
    h1{
        color: #e50914;
        font-size: 3rem;
    }
}
</style>