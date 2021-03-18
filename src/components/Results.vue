<template>
  <div class="container py-3">
    <!--<div class="grid-container my-3">
      <Card v-for="(movie, index) in movies" :key="index" :movie="movie" />
    </div>-->
    <p>Resultados</p>
  </div>
</template>

<script>
//import Card from './Card.vue';

export default {
  name: 'Results',
  components: {},
  props: {
    movies: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style>
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(10rem, 1fr));
  gap: 0.5rem;
}
</style>
