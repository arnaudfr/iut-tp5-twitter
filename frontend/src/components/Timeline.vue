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
import Tweet from './Tweet'
export default {
  components: {Tweet},
  name: 'timeline',
  data () {
    return {
      msg: 'Timeline Twitter',
      tweets: [
      { auteur: 'John Doe', contenu: 'A girl is no one' },
      { auteur: 'Barack Obama', contenu: 'Zinedine Zidane is the raddiest man in the world.' },
      { auteur: 'George Orwell', contenu: 'We are watching' }]
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
