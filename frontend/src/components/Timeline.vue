<template>
  <div class="timeline">
    <h1>{{ msg }}</h1>
    <Utilisateur :utilisateurs="utilisateurs" @cur_user="connected_user"/>
    <p> Utilisateur connecté : {{ current_user }} </p>
    <div v-if="loading">Chargement des tweets en cours…</div>
    <div v-else>
      <feed :tweets="tweets" :current_user="current_user" @retweeted="retweet" />
    </div>
  </div>
</template>

<script>

// Imports
import Feed from './Feed'
import Utilisateur from './Utilisateur'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  name: 'timeline',
  components: {Feed, Utilisateur},

  data () {
    return {
      msg: 'Timeline Zinedine Twitter',
      utilisateurs: [],
      tweets: [],
      current_user: 'No one',
      loading: true
    }
  },

  created () {
    this.fetchTweets()
    this.fetchUsers()
  },

  methods: {
    fetchTweets: function () {
      // GET /list
      this.$http.get('http://localhost:8080/list').then(response => {
        // get body data
        this.tweets = response.body
        this.loading = false
        console.log(response)
      }, response => {
        this.loading = true
      })
    },

    fetchUsers: function () {
      // GET /utilisateurs
      this.$http.get('http://localhost:8080/utilisateurs').then(response => {
        // get body data
        this.utilisateurs = response.body
      }, response => {
      // error callback
      })
    },

    retweet: function (id) {
      for (var i = 0; i <= this.tweets.length; i++) {
        if (this.tweets[i].id === id) {
          this.tweets[i].retweeters.push(this.current_user)
        }
      }
    },

    connected_user: function (user) {
      this.current_user = user
      this.$emit('cur_user', user)
    }
  }
}
</script>

<style scoed>

</style>
