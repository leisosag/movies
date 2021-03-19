<template>
  <div @click="cardSelect" class="container my-3">
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
  methods: {
    cardSelect(e) {
      this.$emit('cardSelected', e.target.alt);
    },
  },
};
</script>

<style>
.card {
  border: none;
  position: relative;
  background-color: transparent;
  border-radius: 0;
  padding: 0.5rem;
}
.card img {
  border-radius: 0;
}
.card:hover {
  cursor: pointer;
  background-color: var(--dark-grey);
}
.card-body {
  padding: 0.2rem;
}
.card-title {
  font-weight: 400;
  font-size: 1rem;
}
</style>
