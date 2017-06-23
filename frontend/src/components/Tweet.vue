<template>
  <div>
    {{ tweet.auteur.prenom }} {{ tweet.auteur.nom }} - {{ tweet.contenu }}
  </div>
</template>

<script>
export default {
  name: 'tweet',
  props: ['tweet']
}
</script>

<style scoped>
</style>
