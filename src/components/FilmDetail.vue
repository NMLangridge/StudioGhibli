<template lang="html">
  <div v-if='film'>
    <h3>{{film.title}}</h3>

    <div id="favourites">
      <button v-on:click="handleClick">Add to Favourites</button>
      <button v-on:click="removeFavourite">Remove from Favourites</button>
    </div>

    <p>Director: {{film.director}}</p>
    <p>Year: {{film.release_date}}</p>
    <p>Description: {{film.description}}</p>
    <p>Critical Reception: {{film.rt_score}}%</p>

  </div>
</template>

<script>
import {eventBus} from "../main.js";
import FilmFilter from "./FilmFilter.vue";

export default {
  name: 'film-detail',
  props: ['film'],
  methods: {
    handleClick(){
      eventBus.$emit('favourite-films', this.film);
    },
    removeFavourite(){
      eventBus.$emit("favourite-removed", this.film);
    }
  }
};
</script>

<style lang="css" scoped>
</style>
