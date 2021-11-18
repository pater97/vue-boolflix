<template>
    <div>
        <section class="search_bar">
            <input v-model="searchText" type="text">
            <button class="search_btn">search</button>
        </section>
    </div>
</template>

<script>
export default {
    data(){
        return{
            searchText:""
        }
    }
}
</script>

<style lang="scss">

</style>