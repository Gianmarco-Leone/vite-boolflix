<script>
// -STATE- Importo file reattivo store.js
import { store } from "../data/store.js";

import AppMovie from "./AppMovie.vue";
import AppSerie from "./AppSerie.vue";

export default {
  data() {
    return {
      store,
    };
  },

  components: {
    AppMovie,
    AppSerie,
  },
};
</script>

<template>
  <main>
    <!-- FILM -->
    <div v-if="store.movies.length" class="my-container p-4">
      <h1 class="text-white mb-5">FILM</h1>
      <ul>
        <AppMovie
          v-for="movie in store.movies"
          :key="movie.id"
          :title="movie.title"
          :originalTitle="movie.original_title"
          :language="movie.original_language"
          :vote="movie.vote_average"
          :pic="movie.poster_path"
          :overview="movie.overview"
        />
      </ul>
    </div>

    <!-- SERIE TV -->
    <div v-if="store.series.length" class="my-container p-4">
      <h1 class="text-white mb-5">SERIE TV</h1>
      <ul>
        <AppSerie
          v-for="serie in store.series"
          :key="serie.id"
          :name="serie.name"
          :originalName="serie.original_name"
          :language="serie.original_language"
          :vote="serie.vote_average"
          :pic="serie.poster_path"
          :overview="serie.overview"
        />
      </ul>
    </div>
  </main>
</template>

<style lang="scss" scoped>
@use "../assets/scss/partials/variables" as *;
main {
  background-color: $dark-color;
  min-height: calc(100vh - 100px);
  padding-top: 3rem;

  ul {
    display: flex;
    flex-wrap: wrap;
    padding-left: 4rem;
    gap: 1rem;
  }
}
</style>
