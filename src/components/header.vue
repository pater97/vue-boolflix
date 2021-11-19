<template>
    <div>
    <h1 class="logo">BOOLFLIX</h1>
     <!-- sezione barra di ricerca   -->
    <section class="search_bar">
      <input
       v-model="searchText"
       type="text"
       placeholder="Search"
       @keyup.enter="$emit('getCall',searchText)" />
      <!-- <button class="search_btn" @click="getCall">search</button> -->
    </section>
    </div>
</template>

<script>
export default {
    data(){
        return{
            searchText : ""
        }
    }
}
</script>

<style lang="scss">
    .logo{
        color: red;
    }
</style>