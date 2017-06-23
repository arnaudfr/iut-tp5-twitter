<template>
  <div class="timeline">
    <h1>{{ msg }}</h1>
    <div v-if="loading">Chargement des tweets en cours…</div>
    <div v-else>
      <feed :tweets="tweets"/>
    </div>
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
      tweets: [],
      loading: true
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
        this.loading = false
        console.log(response)
      }, response => {
        this.loading = true
      })
    }
  }
}
</script>

<style scoed>

</style>
