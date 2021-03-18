<template>
  <div id="app">
    <Header />
    <SearchBar @searchMovie="searchMovie" />
    <!--<Results v-if="isSearchCompleted" :movies="similarMovies" />-->
    <!--<Results v-if="isSearchCompleted" :movies="similarMovies" />-->
    <Results v-if="isSearchCompleted" />
  </div>
</template>

<script>
import axios from 'axios';
import Header from './components/Header.vue';
import SearchBar from './components/SearchBar.vue';
import Results from './components/Results.vue';
const API_KEY = '75cc39d7bd84e6d20a29d9077c5b3d2d';

export default {
  name: 'App',
  components: { Header, SearchBar, Results },
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
:root {
  --bgcolor: #000;
  --black: #211f1f;
  --grey: #292f33;
  --white: #f5f5f1;
  --red: #e50914;
  --red-hover: #cf0812;
}
#app {
  min-height: 100vh;
  background-color: var(--bgcolor);
  color: var(--white);
}
.btn-danger,
.btn-outline-light {
  background-color: var(--red);
  border-radius: 0;
  padding: 0.5rem 1rem;
  text-transform: uppercase;
  font-size: 1rem;
  font-weight: 600;
  color: var(--white);
}
.btn-danger:hover {
  background-color: var(--red-hover);
}
.btn-outline-light {
  color: var(--white);
  background-color: transparent;
  border: 1px solid var(--white);
}
.btn-outline-light :hover {
  background-color: var(--white);
  color: var(--black);
}
</style>
