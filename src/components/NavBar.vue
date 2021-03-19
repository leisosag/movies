<template>
  <div id="navbar">
    <div class="container">
      <nav
        class="navbar navbar-expand-lg navbar-dark fixed-top"
        style="background-color: #000"
      >
        <a class="navbar-brand mx-5" href="/">
          <img
            src="../assets/logo2.png"
            width="30"
            height="30"
            class="d-inline-block align-top mr-1"
            alt=""
          />
          MoviesDB
        </a>
        <form
          @submit.prevent="termSubmit"
          class="form-inline mx-5 ml-auto my-lg-0"
        >
          <input
            onfocus="this.value=''"
            class="form-control mr-2"
            type="text"
            id="searchInput"
            placeholder="Busca una pelicula"
          />
          <button class="btn btn-danger ml-3" type="submit">
            <i class="fas fa-search mr-2"></i>Buscar
          </button>
        </form>
      </nav>
    </div>
  </div>
</template>
<script>
export default {
  name: 'NavBar',
  methods: {
    termSubmit(e) {
      this.$emit('searchMovie', e.target[0].value);
    },
  },
};
</script>
<style>
#navbar {
  background-color: var(--bgdark);
  min-height: 10vh;
  width: 100%;
}
input[type='text'] {
  text-transform: capitalize;
}
</style>
