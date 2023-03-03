<script>
// Importo axios per fare chiamata API
import axios from "axios";

import AppHeader from "./components/AppHeader.vue";
export default {
  data() {
    return {
      moviesEndpoint:
        "https://api.themoviedb.org/3/search/movie?api_key=9e6d26513f128e25f1d7dea31384230a",
    };
  },
  components: {
    AppHeader,
  },
  methods: {
    fetchFilms(url) {
      axios.get(url).then((response) => {
        console.log(response);
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
</template>

<style lang="scss"></style>

<!-- `${this.moviesEndpoint}api_key=${this.api_key}&query=ritorno+al+futuro` -->
