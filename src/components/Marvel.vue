<template>
  <div>
    <h1>Find the heroes you like !</h1>
    <!-- Form -->
    <form v-on:submit="getHero" id="form-twitch">
      <input type="text" name="username" v-model="name">
      <button type="submit">Search</button>
    </form> 
    <!-- Condition -->
    <div v-if="hero !== null">
      <h2>{{hero[0].name}}</h2>
    <!-- List -->
    <div>
      <ul id="list">
        <li v-for="heros in hero">
          <p><span>Who is he/she ? :</span> {{heros.description}}</p>
          <p><span>Where to find him/her ? :</span> {{heros.comics.items[0].name}}</p>
          <p>{{heros.comics.items[1].name}}</p>
          <p>{{heros.comics.items[2].name}}</p>
          <p>{{heros.comics.items[3].name}}</p>
          <p>{{heros.comics.items[4].name}}</p>
          <p>{{heros.comics.items[5].name}}</p>
          <p>{{heros.comics.items[6].name}}</p>
          <p>{{heros.comics.items[7].name}}</p>
          <p>{{heros.comics.items[8].name}}</p>
          <p>{{heros.comics.items[9].name}}</p>
          <p>{{heros.comics.items[10].name}}</p>
          <p>{{heros.comics.items[11].name}}</p>
          <p>{{heros.comics.items[12].name}}</p>
          <p>{{heros.comics.items[13].name}}</p>
          <p>{{heros.comics.items[14].name}}</p>
          <p>{{heros.comics.items[15].name}}</p>
          <p>{{heros.comics.items[16].name}}</p>
          <p>{{heros.comics.items[17].name}}</p>
          <p>{{heros.comics.items[18].name}}</p>
          <p>{{heros.comics.items[19].name}}</p>
        </li>
      </ul>
    </div>
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
console.log(hero);
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

span {
  font-weight: bold;
}
</style>
