<template>
  <div id="app" class="app">
    <RandomQuote></RandomQuote>
  </div>
</template>

<script>
import RandomQuote from './components/RandomQuote.vue'

import 'css-star-rating/css/star-rating.min.css'

export default {
  name: 'app',
  components: {
    RandomQuote,
  },
}
</script>

<style lang="scss">
html,
body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

body {
  color: #ccc;
  background-color: #222;
  font-family: 'Merriweather', arial, sans-serif;
}

.app {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
}
</style>
