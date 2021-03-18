<template>
  <div class="container py-5" id="cards-container">
    <div class="row justify-content-between">
      <h4 class="">Peliculas similares a {{ movieTitle }}</h4>
      <div class="col-12">
        <div class="grid-container my-3">
          <Card
            v-for="(movie, index) in similarMovies"
            :key="index"
            :movie="movie"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Card from './Card.vue';

export default {
  name: 'CardsContainer',
  components: { Card },
  props: {
    similarMovies: {
      type: Array,
      required: true,
    },
    movieTitle: {
      type: String,
      required: true,
    },
  },
};
</script>

<style>
#cards-container {
  min-height: 40vh;
}
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(10rem, 1fr));
  gap: 0.5rem;
}
#cards-container h4 {
  color: var(--grey);
  font-size: 1.5rem;
  margin-bottom: -1rem;
}
</style>
