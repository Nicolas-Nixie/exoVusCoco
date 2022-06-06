<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Selectionnez vos épisodes</h2>
    <ul id="episode">
      <li v-for="episode in episodes" :key="episode.id">
      <span>{{ episode.episode }}</span><br/>
      <span>{{ episode.air_date }}</span><br/>
      <span>{{ episode.name }}</span><br/><br/>
      <button @click="afficPerso(numPerso(episode))">Personnages</button><br/>  
      <span>{{ charName }}</span><br/>
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
      tabPersoFin: null,
      charName: null
    }
  },

  methods: {
    afficPerso(listNumChar, charName) {
      //let tabTempPerso = []
      let paramChar = listNumChar.join(',')
      axios.get('https://rickandmortyapi.com/api/character/' + paramChar)
          .then(response => this.charName = response.data)
      
    for (let i = 0; i < this.charName.length; i++) {
        console.log('je suis dans dans ma fonction reqChar' )
        //tabTempPerso.push(charName[i].this.name)
      }
      
      //tabPersoFin = tabTempPerso.join(',')
    return /*tabPersoFin*/ charName
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
