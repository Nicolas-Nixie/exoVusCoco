<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Selectionnez vos épisodes</h2>
    <ul id="episode">
      <li v-for="episode in episodes" :key="episode.id">
      <span>{{ episode.episode }}</span><br/>
      <span>{{ episode.air_date }}</span><br/>
      <span>{{ episode.name }}</span><br/><br/>
      <button @click="afficPerso(episode)">Personnages</button><br/><br/>
      <span>{{ episode.characters_names }}</span><br/>
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
      episodes: [],
      charNames: []
    }
  },

  methods: {
    afficPerso(episode) {

      let listNumChar = this.numPerso(episode)
      let tabTempPerso = []
      let paramChar = listNumChar.join(',')
      axios.get('https://rickandmortyapi.com/api/character/' + paramChar)
          .then((response) => {
              this.charNames = response.data
              
              for (let i = 0; i < this.charNames.length; i++) {
                tabTempPerso.push(this.charNames[i].name)
              }
          episode.characters_names = tabTempPerso
          this.$forceUpdate() 
          })   
    },

    numPerso(episode) {
      const Number = /[0-9]+$/g
      let listNumChar = []

      for (let i = 0; i < episode.characters.length; i++){
        let charNumber = episode.characters[i].match(Number)
        listNumChar.push(charNumber[0])
      }
      return listNumChar
    },
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
  color: #06120c;
}
h2 {
  margin: 40px 0 0;
  color: #06120c;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
  color: #06120c
}
p {
  color: #06120c;
}
</style>
