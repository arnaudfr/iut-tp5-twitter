<template>
  <div class="timeline">
    <h1>{{ msg }}</h1>
    <ul>
      <li v-for="tweet in tweets">
        <tweet :tweet="tweet"/>
      </li>
    </ul>
  </div>
</template>

<script>

// Imports
import Vue from 'vue'
import Resource from 'vue-resource'
import Tweet from './Tweet'
Vue.use(Resource)

export default {
  name: 'timeline',
  components: {Tweet},

  data () {
    return {
      msg: 'Timeline Twitter',
      tweets: []
    }
  },

  created () {
    this.fetchTweets()
  },

  methods: {
    fetchTweets: function () {
      // GET /list
      this.$http.get('http://localhost:8080/list').then(response => {
        // get body data
        this.tweets = response.body
        console.log(response)
      }, response => {
        this.tweets = { auteur: 'erreur', contenu: '0' }
      })
    }
  }
}
</script>

<style scoed>
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: block;
    margin: 0 10px;
  }

</style>
