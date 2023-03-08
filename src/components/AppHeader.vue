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
  <header>
    <nav class="navbar bg-dark">
      <div class="container-fluid">
        <!-- LOGO  -->
        <a class="navbar-brand fw-semibold fs-1" href="#"> BOOLFLIX </a>

        <!-- CAMPO RICERCA -->
        <form @submit.prevent="search" class="d-flex" role="search">
          <input
            v-model="term"
            class="form-control me-2"
            type="search"
            placeholder="Inserisci nome film/serie ..."
            aria-label="Search"
            @keyup.enter="search"
          />
          <button @click="search()" type="button" class="btn my-btn">
            Cerca
          </button>
        </form>
      </div>
    </nav>
  </header>
</template>

<style lang="scss" scoped>
@use "../assets/scss/partials/variables" as *;
header {
  height: 100px;
  border-bottom: 1px solid #fefefe;

  nav {
    height: 100%;

    a {
      color: $primary-color;
    }

    form {
      input {
        width: 300px;
      }
      .my-btn {
        color: #fff;
        border-color: currentColor;

        &:hover {
          color: $dark-color;
          border-color: currentColor;
          background-color: #fff;
        }
      }
    }
  }
}
</style>
