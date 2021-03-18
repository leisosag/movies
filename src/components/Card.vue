<template>
  <div class="container my-3">
    <div class="card">
      <img :src="imgUrl" class="card-img-top" :alt="movie.title" />
      <div class="card-body">
        <h5 class="card-title">{{ movie.title }}</h5>
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
  border: none;
  position: relative;
  background-color: transparent;
  border-radius: 1rem;
  padding: 0.5rem;
}
.card img {
  border-radius: 1rem;
}
.card:hover {
  cursor: pointer;
  background-color: var(--red);
}
.card-body {
  padding: 0.2rem;
}
.card-title {
  font-weight: 400;
  font-size: 1rem;
}
</style>
