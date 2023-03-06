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
  <nav class="navbar bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand text-danger fw-semibold fs-1" href="#">
        BOOLFLIX
      </a>
      <form class="d-flex" role="search">
        <input
          v-model="term"
          class="form-control me-2"
          type="search"
          placeholder="Inserisci nome film/serie ..."
          aria-label="Search"
        />
        <button @click="search()" type="button" class="btn my-btn">
          Cerca
        </button>
      </form>
    </div>
  </nav>
</template>

<style lang="scss" scoped>
nav {
  .my-btn {
    color: #fff;
    border-color: #fff;
  }
}
</style>
