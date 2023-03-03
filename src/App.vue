<script>
// Importo axios per fare chiamata API
import axios from "axios";

// -STATE- Importo file reattivo store.js
import { store } from "./data/store.js";

import AppHeader from "./components/AppHeader.vue";
import MoviesList from "./components/MoviesList.vue";

export default {
  data() {
    return {
      store,
      moviesEndpoint:
        "https://api.themoviedb.org/3/search/movie?api_key=9e6d26513f128e25f1d7dea31384230a&language=it-IT",
    };
  },
  components: {
    AppHeader,
    MoviesList,
  },
  methods: {
    fetchFilms(url) {
      axios.get(url).then((response) => {
        store.movies = response.data.results;
      });
    },

    fetchFilteredMovies(term) {
      this.fetchFilms(`${this.moviesEndpoint}&query=${term}`);
    },
  },
};
</script>

<template>
  <!-- HEADER -->
  <AppHeader @on-search="fetchFilteredMovies" />

  <!-- MAIN -->
  <MoviesList />
</template>

<style lang="scss">
@use "./assets/scss/style.scss";
</style>

<!-- `${this.moviesEndpoint}api_key=${this.api_key}&query=ritorno+al+futuro` -->
