<template>
  <div>
    <h1>Find the heroes you like !</h1>
    <form v-on:submit="getHero" id="form-twitch">
      <input type="text" name="username" v-model="name">
      <button type="submit">Search</button>
    </form> 
    <div v-if="hero !== null">
      <h2>{{hero[0].name}}</h2>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import CryptoJS from 'crypto-js'

export default {
  data () {
    return {
      name: '',
      hero: null
    }
  },
  methods: {
    getHero: function(e) {
      let ts = new Date().getTime();
      let hash = CryptoJS.MD5(ts + 'SECRET-KEY' + 'API-KEY').toString();
      e.preventDefault()
      let hero = axios.get(`https://gateway.marvel.com/v1/public/characters?name=${this.name}&ts=${ts}&apikey=API-KEY&hash=${hash}`)
          .then(res => res.data.data.results)
          .catch(err => err ? console.error(err) : null)
        hero.then(data => this.hero = data)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: bold;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
