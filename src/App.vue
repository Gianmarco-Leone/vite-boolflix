<script>
// Importo axios per fare chiamata API
import axios from "axios";

// -STATE- Importo file reattivo store.js
import { store } from "./data/store.js";

import AppHeader from "./components/AppHeader.vue";
import MoviesList from "./components/MoviesList.vue";
import SeriesList from "./components/SeriesList.vue";

export default {
  data() {
    return {
      store,
      moviesEndpoint:
        "https://api.themoviedb.org/3/search/movie?api_key=9e6d26513f128e25f1d7dea31384230a&language=it-IT",
      seriesEndpoint:
        "https://api.themoviedb.org/3/search/tv?api_key=9e6d26513f128e25f1d7dea31384230a&language=it-IT",
    };
  },
  components: {
    AppHeader,
    MoviesList,
    SeriesList,
  },
  methods: {
    fetchMoviesResult(url) {
      axios.get(url).then((response) => {
        store.movies = response.data.results;
      });
    },

    fetchSeriesResult(url) {
      axios.get(url).then((response) => {
        store.series = response.data.results;
      });
    },

    fetchFiltered(term) {
      this.fetchMoviesResult(`${this.moviesEndpoint}&query=${term}`);
      this.fetchSeriesResult(`${this.seriesEndpoint}&query=${term}`);
    },
  },
};
</script>

<template>
  <!-- HEADER -->
  <AppHeader @on-search="fetchFiltered" />

  <!-- MAIN -->
  <MoviesList />
  <SeriesList />
</template>

<style lang="scss">
@use "./assets/scss/style.scss";
</style>
