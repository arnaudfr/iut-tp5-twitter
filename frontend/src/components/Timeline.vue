<template>
  <div class="timeline">
    <h1>{{ msg }}</h1>
    <feed :tweets="tweets"/>
  </div>
</template>

<script>

// Imports
import Feed from './Feed'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  name: 'timeline',
  components: {Feed},

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
