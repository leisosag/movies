<template>
  <div class="container py-5">
    <div
      class="row d-flex flex-column justify-content-center align-items-center"
      id="header"
    >
      <div class="col-md-6">
        <form @submit.prevent="termSubmit" class="d-flex">
          <label for="searchInput" class="sr-only">Search movies</label>
          <input
            onfocus="this.value=''"
            class="form-control ml-2"
            type="text"
            id="searchInput"
            placeholder="Busca una pelicula"
          />
          <button class="btn btn-danger ml-3" type="submit">
            <i class="fas fa-search mr-2"></i>Buscar
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  methods: {
    termSubmit(e) {
      this.$emit('searchMovie', e.target[0].value);
    },
  },
};
</script>

<style scoped>
.btn-danger {
  min-width: 8rem;
}
</style>
