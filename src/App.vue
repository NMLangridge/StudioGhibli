<template lang="html">
  <div id="app">
    <h1>Studio Ghibli</h1>
    <h2>Films</h2>
    <div id="list-info"
    <films-list :films='films'></films-list>
    <film-detail :film='selectedFilm'></film-detail>
    <favourite-films :films='favouriteFilms'></favourite-films>
    <film-filter :films="films"></film-filter>
  </div>
</div>
</template>

<script>
import {eventBus} from "./main.js";
import FilmsList from "./components/FilmsList.vue";
import FilmDetail from "./components/FilmDetail.vue";
import FavouriteFilms from "./components/FavouriteFilms.vue";
import FilmFilter from "./components/FilmFilter.vue";

export default {
  name: 'app',
  data(){
    return {
      films: [],
      selectedFilm: null,
      favouriteFilms: [],
      favouriteRemoved: []
    };
  },

  mounted(){
    fetch('https://ghibliapi.herokuapp.com/films/')
    .then(result => result.json())
    .then(films => this.films = films)

    eventBus.$on('selected-film', (film) => {
      this.selectedFilm = film;
    })

    eventBus.$on('favourite-films', (film) => {
      this.favouriteFilms.push(film);
    })

    eventBus.$on('favourite-removed', (film) => {
      this.favouriteFilms.pop(film);
    })

  },
  components: {
    "films-list": FilmsList,
    "film-detail": FilmDetail,
    "favourite-films": FavouriteFilms,
    "film-filter": FilmFilter
  }
}
</script>

<style lang="css" scoped>
/* #app {
  background-color: lightblue;
}

#list-info {
  display: flex;
} */
</style>

<!-- result = this.favouriteFilms.indexOf(film)
this.favouriteFilms.splice(result, 1) -->
