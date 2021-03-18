<template>
  <div class="container py-3">
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
          <button class="btn btn-danger ml-3" type="submit">Buscar</button>
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

<style>
#header {
  min-height: 30vh;
  width: 100%;
}
</style>
