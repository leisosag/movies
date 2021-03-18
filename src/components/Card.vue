<template>
  <div class="container my-3">
    <div class="card">
      <img :src="imgUrl" class="card-img-top" :alt="movie.title" />
      <div class="card-body">
        <h5 class="card-title">{{ movie.title }}</h5>
        <p class="card-text">{{ movie.overview }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
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

<style>
.card {
}
</style>
