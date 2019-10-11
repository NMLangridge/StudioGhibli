<template lang="html">
  <div id="favourites" v-if='films'>
    <h2>Favourites</h2>
    <ul>
      <li v-for='favourite in films'>{{favourite.title}}</li>
    </ul>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'favourite-films',
  props: ['films']
}
</script>

<style lang="css" scoped>
#favourites {
  position: absolute;
  right: 50%;
  top: 55px;
}
</style>
