<template>
  <div id="app">
    <img src="./assets/marvel.jpg">
    <marvel></marvel>   
  </div>
</template>

<script>
import Marvel from './components/Marvel'

export default {
  name: 'app',
  components: {
    Marvel
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#app img {
  width: 20%;
}
</style>
