<template>
  <div id="app">
    <NavBar />

    <Header />
    <SearchBar @searchMovie="searchMovie" />
    <MovieDetails
      v-if="isSearchCompleted"
      :movie="movie"
      :genreNames="genreNames"
      @searchSimilar="searchSimilar"
    />
    <CardsContainer
      v-if="isSearchSimilar"
      :similarMovies="similarMovies"
      :movieTitle="movieTitle"
    />
    <!--<Results v-if="isSearchCompleted" :movies="similarMovies" />-->
    <!--<Results v-if="isSearchCompleted" :movies="similarMovies" />-->
  </div>
</template>

<script>
import axios from 'axios';
import NavBar from './components/NavBar.vue';
import Header from './components/Header.vue';
import SearchBar from './components/SearchBar.vue';
import MovieDetails from './components/MovieDetails.vue';
import CardsContainer from './components/CardsContainer.vue';
const API_KEY = '75cc39d7bd84e6d20a29d9077c5b3d2d';

export default {
  name: 'App',
  components: {
    NavBar,
    Header,
    SearchBar,
    MovieDetails,
    CardsContainer,
  },
  data() {
    return {
      isSearchCompleted: false,
      isSearchSimilar: false,
      movie: {},
      similarMovies: [],
      genres: [],
      genreNames: [],
      movieTitle: '',
    };
  },
  methods: {
    //get genres
    getGenres() {
      try {
        axios
          .get(
            `https://api.themoviedb.org/3/genre/movie/list?api_key=${API_KEY}&language=en-US`
          )
          .then((response) => {
            this.genres = response.data.genres;
          });
      } catch (error) {
        console.error(error);
      }
    },
    //filter genres
    filterGenres(ids) {
      this.genreNames = [];
      this.genres.forEach((genre) => {
        for (let i = 0; i < ids.length; i++) {
          ids[i] === genre.id ? this.genreNames.push(genre.name) : null;
        }
      });
    },
    // gets movie details
    searchMovie(term) {
      this.isSearchCompleted = false;

      try {
        axios
          .get(
            `https://api.themoviedb.org/3/search/movie?api_key=${API_KEY}&language=en-US&page=1&include_adult=false&query=${term}`
          )
          .then((response) => {
            this.movie = response.data.results[0];
            this.filterGenres(this.movie.genre_ids);
            this.isSearchCompleted = true;
            this.movieTitle = '';
            this.isSearchSimilar = false;
          });
      } catch (error) {
        console.log(error);
      }
    },

    // gets recommended movies
    searchSimilar(id, title) {
      this.isSearchSimilar = false;
      this.movieTitle = title;

      try {
        axios
          .get(
            `https://api.themoviedb.org/3/movie/${id}/similar?api_key=${API_KEY}&language=en-US&page=1`
          )
          .then((response) => {
            this.similarMovies = response.data.results;
            this.isSearchSimilar = true;
          });
      } catch (error) {
        console.error(error);
      }
    },
  },
  created() {
    this.getGenres();
  },
};
</script>

<style>
:root {
  --bgdark: #000;
  --black: #211f1f;
  --grey: #292f33;
  --grey: #bbb;
  --white: #f5f5f1;
  --red: #e50914;
  --red-hover: #cf0812;
}
#app {
  min-height: 100vh;
  background-color: var(--bgdark);
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
.btn-outline-danger {
  border-radius: 0;
}
.btn-outline-danger:hover {
  background-color: var(--red);
}
</style>
