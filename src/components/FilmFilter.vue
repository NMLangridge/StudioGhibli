<template lang="html">

  <form v-on:submit.prevent>
    <input type="text" v-model="search" placeholder="Search for film..." v-on:keyup="searchForFilm">
    <select v-on:change="handleSelect" v-model="selectedFilm">
      <option disabled value="">Select a film</option>
      <option v-for="film in films" :value="film">{{film.title}}</option>
    </select>
  </form>

</template>

<script>
import {eventBus} from '../main.js';
import ListItem from "./ListItem.vue";
import FilmsList from "./FilmsList.vue";

export default {
  name: "film-filter",
  data(){
    return {
      search: "",
      selectedFilm: null,
      favouriteFilms: []
    }
  },
  props: ["films"],
  methods: {
    searchForFilm(){
      let foundFilm = this.films.find((film) => {
        return film.title.toLowerCase().indexOf(this.search.toLowerCase()) > -1
      })
      this.selectedFilm = foundFilm

      eventBus.$emit('selected-film', this.selectedFilm)
    },
    handleSelect(){
      this.search = ""
      eventBus.$emit('selected-film', this.selectedFilm)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
