
<!-- script goes here -->
<script>

import LinkShortner from './components/LinkShortner.vue'
export default {
  name: 'App',
  components: {
    LinkShortner
  }
}
</script>

<!-- view goes here -->
<template>
  <div id="app">
    <LinkShortner></LinkShortner>
  </div>
</template>

<!-- styles goes here -->
<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Bebas Neue', cursive;
}

@media (min-width: 1024px) {
 
}
</style>
