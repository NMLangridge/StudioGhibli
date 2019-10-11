<template lang="html">
  <div>
    <li v-on:click="handleClick">{{film.title}}</li>
  </div>
</template>

<script>
import {eventBus} from "../main.js";

export default {
  name: 'list-item',
  props: ['film'],
  methods: {
    handleClick(){
      eventBus.$emit('film-selected', this.film)
    },
    mounted(){
      eventBus.$on('film-selected', (film) => {
        this.film = film
      })
    }
  }
}
</script>

<style lang="css" scoped>
</style>
