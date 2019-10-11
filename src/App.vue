<template lang="html">
  <div>
    <h1>Studio Ghibli</h1>
    <h2>Films</h2>
    <films-list :films='films'></films-list>
    <film-detail :film='selectedFilm'></film-detail>
    <favourite-films :films='favouriteFilms'></favourite-films>
    <film-filter :films="films"></film-filter>
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
      favouriteFilms: []
    };
  },
  // methods: {
  //   markFavourite: function(beer) {
  //     const index = this.beers.indexOf(beer);
  //     this.beers[index].isFavourite = true;
  //   },
  //   unmarkFavourite: function(film) {
  //     const index = this.films.indexOf(film);
  //     this.films[index].isFavourite = false;
  //   },
  // },
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

    eventBus.$on('favourite-removed', film => {
      this.unmarkFavourite(film);
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
</style>







markFavourite: function(beer) {
  const index = this.beers.indexOf(beer);
  this.beers[index].isFavourite = true;
},
unmarkFavourite: function(beer) {
  const index = this.beers.indexOf(beer);
  this.beers[index].isFavourite = false;
}
},
mounted() {
  this.getBeers();

  eventBus.$on("beer-selected", beer => (this.selectedBeer = beer));

  eventBus.$on("favourite-added", beer => this.markFavourite(beer));

  eventBus.$on("favourite-removed", beer => this.unmarkFavourite(beer));
}
};
