<template>
  <div class="hero is-fullheight is-bold is-link" id="app">
    <SearchImageComponent />
  </div>
</template>

<script>

import SearchImageComponent from './components/SearchImageComponent.vue'

export default {
  name: 'app',
  components: {
    SearchImageComponent
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
