<script>
// Importo axios per fare chiamata API
import axios from "axios";

// -STATE- Importo file reattivo store.js
import { store } from "./data/store.js";

import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";

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
    AppMain,
  },
  methods: {
    fetchMoviesResult(url) {
      store.movies = [];
      axios.get(url).then((response) => {
        // Utilizzo map per salvare solo informazioni che mi servono
        const films = response.data.results.map((film) => {
          return {
            title: film.title,
            originalTitle: film.original_title,
            language: film.original_language,
            vote: film.vote_average,
            pic: film.poster_path,
            overview: film.overview,
            id: film.id,
            cast: [],
            genres: [],
          };
        });

        films.forEach((film) => {
          // API Cast
          axios
            .get(
              `https://api.themoviedb.org/3/movie/${film.id}/credits?api_key=9e6d26513f128e25f1d7dea31384230a`
            )
            .then((element) => {
              for (let i = 0; i < 5; i++) {
                film.cast.push(element.data.cast[i].name);
              }
            });

          // API Genres
          axios
            .get(
              `https://api.themoviedb.org/3/movie/${film.id}?api_key=9e6d26513f128e25f1d7dea31384230a`
            )
            .then((element) => {
              film.genres.push(element.data.genres);
            });
        });
        store.movies = films;
      });
    },

    fetchSeriesResult(url) {
      store.series = [];
      axios.get(url).then((response) => {
        // Utilizzo map per salvare solo informazioni che mi servono
        const series = response.data.results.map((serie) => {
          return {
            title: serie.name,
            originalTitle: serie.original_name,
            language: serie.original_language,
            vote: serie.vote_average,
            pic: serie.poster_path,
            overview: serie.overview,
            id: serie.id,
            cast: [],
          };
        });

        series.forEach((serie) => {
          axios
            .get(
              `https://api.themoviedb.org/3/tv/${serie.id}/credits?api_key=9e6d26513f128e25f1d7dea31384230a`
            )
            .then((element) => {
              for (let i = 0; i < 5; i++) {
                if (element.data.cast.length) {
                  serie.cast.push(element.data.cast[i].name);
                }
              }
            });
        });
        store.series = series;
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
  <AppMain />
</template>

<style lang="scss">
@use "./assets/scss/style.scss";
</style>
