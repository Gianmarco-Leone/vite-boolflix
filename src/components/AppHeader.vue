<script>
export default {
  data() {
    return {
      term: "",
    };
  },
  emits: ["on-search"],
  methods: {
    search() {
      this.$emit("on-search", this.term);
    },
  },
};
</script>

<template>
  <form action="">
    <input
      v-model="term"
      type="text"
      placeholder="Inserisci nome film/serie ..."
    />
    <button @click="search()" type="button">Cerca</button>
  </form>
</template>

<style lang="scss" scoped></style>
