<script>
// -STATE- Importo file reattivo store.js
import { store } from "../data/store.js";

import AppMovie from "./AppMovie.vue";

export default {
  data() {
    return {
      store,
    };
  },

  components: {
    AppMovie,
  },
};
</script>

<template>
  <h1>Film:</h1>
  <ul>
    <AppMovie
      v-for="movie in store.movies"
      :key="movie.id"
      :title="movie.title"
      :originalTitle="movie.original_title"
      :language="movie.original_language"
      :vote="movie.vote_average"
      :pic="movie.poster_path"
    />
  </ul>
</template>

<style lang="scss" scoped>
ul {
  display: flex;
  flex-wrap: wrap;
}
</style>
