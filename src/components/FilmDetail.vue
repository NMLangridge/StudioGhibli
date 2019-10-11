<template lang="html">
  <div v-if='film'>
    <h3>{{film.title}}</h3>

    <p>Director: {{film.director}}</p>
    <p>Year: {{film.release_date}}</p>
    <p>Critical Reception: {{film.rt_score}}%<p>
    <p>Description: {{film.description}}</p>

  </div>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: 'film-detail',
  props: ['film']
}
</script>

<style lang="css" scoped>
</style>
