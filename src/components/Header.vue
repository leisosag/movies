<template>
  <div class="container">
    <div
      class="row d-flex flex-column justify-content-center align-items-center"
      id="header"
    >
      <h1>Y ahora que veo?</h1>
      <p>Busca una pelicula</p>

      <div class="col-md-8">
        <form @submit.prevent="termSubmit" class="d-flex">
          <label for="searchInput" class="sr-only">Search movies</label>
          <input
            onfocus="this.value=''"
            class="form-control ml-2"
            type="text"
            id="searchInput"
            placeholder="Busca una pelicula"
          />
          <button class="btn btn-outline-danger ml-3" type="submit">
            Buscar
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Header',
  methods: {
    termSubmit(e) {
      this.$emit('searchMovie', e.target[0].value);
    },
  },
};
</script>

<style>
#header {
  min-height: 50vh;
  width: 100%;
}
</style>
