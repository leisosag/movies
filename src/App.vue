<template>
  <div id="app">
    <Header @searchMovie="searchMovie" />
    <!--<Results v-if="isSearchCompleted" :movies="similarMovies" />-->
    <Results v-if="isSearchCompleted" :movies="similarMovies" />
  </div>
</template>

<script>
import axios from 'axios';
import Header from './components/Header.vue';
import Results from './components/Results.vue';
const API_KEY = '75cc39d7bd84e6d20a29d9077c5b3d2d';

export default {
  name: 'App',
  components: { Header, Results },
  data() {
    return {
      isSearchCompleted: false,
      movieId: 0,
      ovies: [],
    };
  },
  methods: {
    searchMovie(term) {
      this.isSearchCompleted = false;
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=${API_KEY}&language=en-US&page=1&include_adult=false&query=${term}`
        )
        .then((response) => {
          this.movieId = response.data.results[0].id;
        })
        .then(() =>
          axios.get(
            `https://api.themoviedb.org/3/movie/${this.movieId}/similar?api_key=${API_KEY}&language=en-US&page=1`
          )
        )
        .then((response) => {
          this.similarMovies = response.data.results;
          this.isSearchCompleted = true;
        });
    },
  },
};
</script>

<style>
#app {
  min-height: 100vh;
}
</style>
