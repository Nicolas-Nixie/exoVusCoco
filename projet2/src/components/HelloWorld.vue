<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Selectionnez vos épisodes</h2>
    <ul id="episode">
      <li v-for="episode in episodes" :key="episode.id">
      <span>{{ episode.episode }}</span><br/>
      <span>{{ episode.air_date }}</span><br/>
      <span>{{ episode.name }}</span><br/>
      <button @click="afficPerso(numPerso(episode))">Personnages</button>
      </li>
    </ul>
  </div>
  
</template>

<script>
const axios = require('axios').default;

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data () {
    return {
      episodes: []
    }
  },

  methods: {
    afficPerso(listNumChar) {
      console.log(listNumChar)
      let paramChar = listNumChar.join(',')
      console.log(paramChar)
      axios.get('https://rickandmortyapi.com/api/character/' + paramChar)
          .then(response => this.name = response.data.name)
    },

    numPerso(episode) {
      const Number = /[0-9]+$/g //regex pas bonne
      let listNumChar = []

      for (let i = 0; i < episode.characters.length; i++){
        let charNumber = episode.characters[i].match(Number)
        listNumChar.push(charNumber[0])
      }
      return listNumChar
    },

    reqChar() {
    axios.get('https://rickandmortyapi.com/api/character/')
      .then(response => this.episodes = response.data)
  }
  },

  created() {
    axios.get('https://rickandmortyapi.com/api/episode/1,2,3,4,5,6,7,8,9,10')
      .then(response => this.episodes = response.data)
  },

  

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  color: #42b983;
}
h2 {
  margin: 40px 0 0;
  color: #42b983;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
  color: #42b983
}
p {
  color: #42b983;
}
</style>
