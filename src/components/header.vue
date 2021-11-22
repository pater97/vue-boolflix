<template>
  <div class="container_header">
      <!-- logo  -->
    <div class="logo">
      <h1>BOOLFLIX</h1>
      <a href="#">Home</a>
      <a href="#">Serie tv</a>
      <a href="#">Film</a>
      <a href="#">Nuovi e popolari</a>
      <a href="#">La mia lista</a>
    </div>
    <!-- sezione barra di ricerca   -->
    <section class="search_bar">
      <input
        v-model="searchText"
        type="text"
        placeholder="Search"
        @keyup.enter="$emit('getCall', searchText)"
      />
      <a href="#">Bambini</a>
      <img class="icon" src="../assets/bell-solid.svg" alt="">
      <img class="avatar" src="../assets/net-avatar.png" alt="">
      <select name="account" id="select_account">
        <option value="#">account 2</option>
        <option value="#">account 3</option>
      </select>
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
  display: flex;
  align-items: center;
    h1{
        color: #e50914;
        font-size: 3rem;
        padding-right: 2rem;
    }
    a{
      color: white;
      text-decoration: none;
      padding:0 .7rem ;
      &:hover{
        filter: brightness(.7);
      }
    }
}
.search_bar{
  display: flex;
  align-items: center;
  .icon{
    width: 1rem;
    filter: invert(1);
    margin: 0 1rem;
  }
  .avatar{
    width: 2rem;
    margin-right: .2rem;
  }
  a{
    text-decoration: none;
    color: white;
    margin-left: 1rem;
  }
  #select_account{
    background-color: transparent;
    border: none;
    color: white;
    width: 1rem;
  }
}
</style>