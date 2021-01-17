<template>
<div id='app'>
<link rel="preconnect" href="https://fonts.gstatic.com">
<link href="https://fonts.googleapis.com/css2?family=Baloo+2&display=swap" rel="stylesheet">
<kanye-quote v-bind:quote='kanyeQuote'></kanye-quote>
<weather-app></weather-app>
</div>
</template>



<script>

// import { eventBus } from './main.js'
import KanyeQuote from './components/KanyeQuote.vue'
import Weather from './components/Weather.vue'

export default {
  name: "app",
  data () {
    return {
      kanyeQuote: undefined
    }
  },

  mounted () {
      fetch ("https://api.kanye.rest/")
      .then (response => response.json())
      .then (kanyeQuote => this.kanyeQuote = kanyeQuote.quote)
  },

  components: {
    "kanye-quote": KanyeQuote,
    "weather-app": Weather

  }
}
</script>

<style>

input {
  margin-bottom: 10px;
}

button {
  font-family: 'Baloo 2', cursive;
  margin: 10px;
}

#app {
  font-family: 'Baloo 2', cursive;
  display: flex;
  justify-content: space-around;
  background-color: black;
}
</style>