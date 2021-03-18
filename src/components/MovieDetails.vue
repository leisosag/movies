<template>
  <div class="container">
    <div class="row">
      <div class="card" style="width: 18rem">
        <img :src="imgUrl" class="card-img-top" :alt="movie.title" />
        <div class="card-body">
          <h5 class="card-title">{{ movie.title }}</h5>
          <a href="#" class="btn btn-danger">Ver peliculas similares</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MovieDetails',
  props: {
    movie: {
      type: Object,
      required: true,
    },
  },
  computed: {
    imgUrl() {
      let path = `https://image.tmdb.org/t/p/w500${this.movie.poster_path}`;
      return path;
    },
  },
};
</script>

<style></style>
