<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Selectionnez vos épisodes</h2>
    <ul id="episode">
      <li v-for="episode in episodes" :key="episode.id">
      <span>{{ episode.id }}</span><br/>
      <span>{{ episode.episode }}</span><br/>
      <span>{{ episode.name }}</span><br/>
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

created() {
  axios.get('https://rickandmortyapi.com/api/episode/1,2,3,4,5,6,7,8,9,10')
    .then(response => this.episodes = response.data)
}

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
