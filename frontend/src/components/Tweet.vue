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
        <a @click="retweet(tweet.id)"><li class="button"><icon name="retweet"/> <span></span></li></a>
        <li class="button"><icon name="heart"/></li>
        <li class="button"><icon name="envelope"/></li>
      </ul>
    </div>
  </div>
</template>

<script>
import 'vue-awesome/icons'
import moment from 'moment'
import Icon from 'vue-awesome/components/Icon'
export default {
  components: {Icon},
  name: 'tweet',
  props: ['tweet'],
  methods: {
    moment: function (date) {
      return moment(date)
    }
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

  span.handle {
   color: gray;
  }
</style>
