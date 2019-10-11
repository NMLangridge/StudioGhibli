<template lang="html">
  <div>
    <h1>Studio Ghibli Films</h1>

    <films-list :films='films'></films-list>
    <film-detail :film='selectedFilm'></film-detail>

  </div>
</template>

<script>
import {eventBus} from "./main.js";
import FilmsList from "./components/FilmsList.vue";
import FilmDetail from "./components/FilmDetail.vue";
// import ListItem from "./components/ListItem.vue";

export default {
  name: 'app',
  data(){
    return {
      films: [],
      selectedFilm: null
    };
  },
  mounted(){
    fetch('https://ghibliapi.herokuapp.com/films/')
    .then(result => result.json())
    .then(films => this.films = films)

    eventBus.$on('film-selected', (film) => {
      this.selectedFilm = film;
    })
  },
  components: {
    "films-list": FilmsList,
    "film-detail": FilmDetail
  }
}
</script>

<style lang="css" scoped>
</style>
