<template>
  <div id="app">
    <siteHeader/>
    <siteMain/>
  </div>
</template>

<script>
import siteHeader from './components/header.vue'
import siteMain from './components/main.vue'
export default {
  name: 'App',
  components: {
  siteMain,
  siteHeader
  }
}
</script>

<style lang="scss">

</style>
