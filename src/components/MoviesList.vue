<script>
// -STATE- Importo file reattivo store.js
import { store } from "../data/store.js";

export default {
  data() {
    return {
      store,
    };
  },
};
</script>

<template>
  <ul>
    <li v-for="movie in store.movies">
      <span> TITLE: {{ movie.title }} </span>
      <br />
      <span> ORIGINAL TITLE: {{ movie.original_title }} </span>
      <br />
      <span> LANGUAGE: {{ movie.original_language }} </span>
      <br />
      <span> VOTE: {{ movie.vote_average }} </span>
    </li>
  </ul>
</template>

<style lang="scss" scoped>
// debug
ul {
  display: flex;
  flex-wrap: wrap;
  li {
    width: 300px;
    border: 1px solid black;
  }
}
</style>
