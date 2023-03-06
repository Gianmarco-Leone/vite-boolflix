<script>
// -STATE- Importo file reattivo store.js
import { store } from "../data/store.js";

import AppSerie from "./AppSerie.vue";

export default {
  data() {
    return {
      store,
    };
  },
  components: {
    AppSerie,
  },
};
</script>

<template>
  <div class="my-container p-4">
    <h1 class="text-white mb-5">SERIE TV:</h1>
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
</template>

<style lang="scss" scoped>
ul {
  display: flex;
  flex-wrap: wrap;
  padding-left: 4rem;
  gap: 1rem;
}
</style>
