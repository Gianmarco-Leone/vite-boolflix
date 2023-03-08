<script>
// -STATE- Importo file reattivo store.js
import { store } from "../data/store.js";

import AppCard from "./AppCard.vue";

export default {
  data() {
    return {
      store,
    };
  },

  components: {
    AppCard,
  },
};
</script>

<template>
  <main>
    <!-- FILM -->
    <div v-if="store.movies.length" class="my-container p-4">
      <h1 class="text-white mb-5">FILM</h1>
      <ul>
        <AppCard
          v-for="movie in store.movies"
          :key="movie.id"
          :title="movie.title"
          :originalTitle="movie.originalTitle"
          :language="movie.language"
          :vote="movie.vote"
          :pic="movie.pic"
          :overview="movie.overview"
          :cast="movie.cast"
        />
      </ul>
    </div>

    <!-- SERIE TV -->
    <div v-if="store.series.length" class="my-container p-4">
      <h1 class="text-white mb-5">SERIE TV</h1>
      <ul>
        <AppCard
          v-for="serie in store.series"
          :key="serie.id"
          :title="serie.title"
          :originalTitle="serie.originalTitle"
          :language="serie.language"
          :vote="serie.vote"
          :pic="serie.pic"
          :overview="serie.overview"
          :cast="serie.cast"
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
