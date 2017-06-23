<template>
  <div class="tweet">
    <div>
      <strong>{{ tweet.auteur.prenom }} {{ tweet.auteur.nom }}</strong>
      <span class="handle">@{{ tweet.auteur.handle }}</span> - {{ moment(tweet.date).fromNow() }}
    </div>
    <div>
      {{ tweet.contenu }}
    </div>
    <div>
      <ul>
        <li class="button"><icon name="reply"/></li>
        <li class="button"><a v-if="retweetable" @click="retweet(tweet.id)"><icon name="retweet"/></a>
        <span class="aside">{{ tweet.retweeters.length }}</span></li>
        <li class="button"><icon name="heart"/></li>
        <li class="button"><icon name="envelope"/></li>
      </ul>
    </div>
  </div>
</template>

<script>
import 'vue-awesome/icons'
import moment from 'moment'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
import Icon from 'vue-awesome/components/Icon'
export default {
  components: {Icon},
  name: 'tweet',
  props: ['tweet', 'current_user'],
  methods: {
    moment: function (date) {
      return moment(date)
    },

    retweet: function (id) {
      var data = new FormData()
      data.append('utilisateur', this.current_user)
      data.append('tweet', id)

      this.$http.post('http://localhost:8080/retweet', data).then(response => {
        this.$emit('retweeted', id)
      }, response => {})
    }

    //retweetable: function (

  },

  created () {
    moment.locale('fr')
  }

}
</script>

<style scoped>
  li.button {
   display: inline-block;
  }

  a {
   color: #42b983;
  }

  span.aside {
    font-size: 0.7em;
  }

  span.handle {
   color: gray;
  }
</style>
