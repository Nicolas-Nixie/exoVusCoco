<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Selectionnez vos épisodes</h2><br/>
    <ul id="episode">
      <li v-for="episode in episodes" :key="episode.id">
      <span>{{ episode.episode }}</span><br/>
      <span>{{ episode.air_date }}</span><br/>
      <span>{{ episode.name }}</span><br/><br/>
      
      <!-- <span>{{ episode.characters_names }}</span><br/> -->

    <h3>Personnages</h3>
    <button @click="afficPerso(episode)">Afficher les personnages</button><br/>
        <table class="rwd-table">
          <thead>
            <tr>
              <th scope="col">Appelation</th>
            </tr>
          </thead>
          <tbody>
            <th scope="row"></th>
            <tr v-for="characters in episode.characters_names" :key="characters.id">
              {{ characters }}
            </tr>
            <!--<td data-th="Characters name">{{ episode.characters_names }}</td>-->
          </tbody>
        </table><br/>
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
      charNames: [],
      
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

  firstName(episode) {
    for (let i = 0; i < episode.characters_names.length; i ++) {
    this.episode.characters_names.split(" ")
}
  }

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

@import "https://fonts.googleapis.com/css?family=Montserrat:300,400,700";
.rwd-table {
  margin: 1em 0;
  min-width: 300px;
}
.rwd-table tr {
  border-top: 1px solid #ddd;
  border-bottom: 1px solid #ddd;
}
.rwd-table th {
  display: none;
}
.rwd-table td {
  display: block;
}
.rwd-table td:first-child {
  padding-top: 0.5em;
}
.rwd-table td:last-child {
  padding-bottom: 0.5em;
}
.rwd-table td:before {
  content: attr(data-th) ": ";
  font-weight: bold;
  width: 6.5em;
  display: inline-block;
}
@media (min-width: 480px) {
  .rwd-table td:before {
    display: none;
  }
}
.rwd-table th,
.rwd-table td {
  text-align: left;
}
@media (min-width: 480px) {
  .rwd-table th,
  .rwd-table td {
    display: table-cell;
    padding: 0.25em 0.5em;
  }
  .rwd-table th:first-child,
  .rwd-table td:first-child {
    padding-left: 0;
  }
  .rwd-table th:last-child,
  .rwd-table td:last-child {
    padding-right: 0;
  }
}

body {
  padding: 0 2em;
  font-family: Montserrat, sans-serif;
  -webkit-font-smoothing: antialiased;
  text-rendering: optimizeLegibility;
  color: #444;
  background: #06120c;
}

h1 {
  font-weight: normal;
  letter-spacing: -1px;
  color: #06120c;
}

.rwd-table {
  background: #0eaeca;
  color: #06120c;
  border-radius: 0.4em;
  overflow: hidden;
}
.rwd-table tr {
  border-color: #06120c;
}
.rwd-table th,
.rwd-table td {
  margin: 0.5em 1em;
  align-content: center;
}
@media (min-width: 480px) {
  .rwd-table th,
  .rwd-table td {
    padding: 1em !important;
  }
}
.rwd-table th,
.rwd-table td:before {
  color: #d3db4a;
}
</style>