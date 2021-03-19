<template>
  <div id="app">
    <NavBar @searchMovie="searchMovie" />
    <Carousel />
    <!-- Popular Movies -->
    <div class="pt-5">
      <CardsContainer
        :movies="popularMovies"
        :title="titlePopular"
        :movieTitle="movieTitle"
        @cardSelected="cardSelected"
      />
    </div>
    <!-- Top Rated Movies -->
    <CardsContainer
      :movies="topMovies"
      :title="titleTop"
      :movieTitle="movieTitle"
      @cardSelected="cardSelected"
    />
    <!-- Upcoming Movies -->
    <CardsContainer
      :movies="upcomingMovies"
      :title="titleUpcoming"
      :movieTitle="movieTitle"
      @cardSelected="cardSelected"
    />
    <!-- Single Movie Details -->
    <MovieDetails
      v-if="isSearchCompleted"
      :movie="movie"
      :genresFound="genresFound"
      @searchSimilar="searchSimilar"
      @getGenre="getByGenre"
    />
    <!-- Similar Movies -->
    <CardsContainer
      v-if="isSearchSimilar"
      :title="titleSimilar"
      :movies="similarMovies"
      :movieTitle="movieTitle"
      @cardSelected="cardSelected"
    />
    <!-- Genre Movies -->
    <CardsContainer
      v-if="isSearchGenre"
      :title="titleGenre"
      :movies="moviesByGenre"
      :movieTitle="movieTitle"
      @cardSelected="cardSelected"
    />
  </div>
</template>

<script>
import axios from 'axios';
import NavBar from './components/NavBar.vue';
import Carousel from './components/Carousel.vue';
import MovieDetails from './components/MovieDetails.vue';
import CardsContainer from './components/CardsContainer.vue';
const API_KEY = '75cc39d7bd84e6d20a29d9077c5b3d2d';

export default {
  name: 'App',
  components: {
    NavBar,
    Carousel,

    MovieDetails,
    CardsContainer,
  },
  data() {
    return {
      isSearchCompleted: false,
      isSearchSimilar: false,
      isSearchGenre: false,
      movie: {},
      similarMovies: [],
      popularMovies: [],
      upcomingMovies: [],
      topMovies: [],
      genres: [],
      genresFound: [],
      moviesByGenre: [],
      movieTitle: '',
      titleSimilar: '',
      titlePopular: '',
      titleTop: '',
      titleUpcoming: '',
      titleGenre: '',
    };
  },
  methods: {
    //get lists of genres
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
      this.genresFound = [];
      this.genres.forEach((genre) => {
        for (let i = 0; i < ids.length; i++) {
          if (ids[i] === genre.id) {
            this.genresFound.push(genre);
          }
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
            this.isSearchGenre = false;
          });
      } catch (error) {
        console.log(error);
      }
    },
    // gets recommended movies
    searchSimilar(id, title) {
      this.isSearchSimilar = false;
      this.movieTitle = title;
      this.titleSimilar = 'Similar Movies';
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
    // gets popular movies
    getMovies(param) {
      try {
        axios
          .get(
            `https://api.themoviedb.org/3/movie/${param}?api_key=${API_KEY}&language=en-US&page=1`
          )
          .then((response) => {
            if (param === 'popular') {
              this.titlePopular = 'Popular Movies';
              this.popularMovies = response.data.results.slice(0, 6);
            }
            if (param === 'top_rated') {
              this.titleTop = 'Top Rated Movies';
              this.topMovies = response.data.results.slice(0, 6);
            }
            if (param === 'upcoming') {
              this.titleUpcoming = 'Upcoming Movies';
              this.upcomingMovies = response.data.results.slice(0, 6);
            }
          });
      } catch (error) {
        console.error(error);
      }
    },
    // gets movies by genre
    getByGenre(id, name) {
      this.moviesByGenre = [];
      this.isSearchGenre = false;
      this.titleGenre = '';
      try {
        axios
          .get(
            `https://api.themoviedb.org/3/discover/movie?api_key=${API_KEY}&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1&with_genres=${id}`
          )
          .then((response) => {
            this.moviesByGenre = response.data.results.slice(0, 6);
            this.isSearchGenre = true;
            this.titleGenre = name;
          });
      } catch (error) {
        console.error(error);
      }
    },
    // when the user clicks on a recommended movie, queries the search with that title
    cardSelected(title) {
      this.searchMovie(title);
    },
  },
  created() {
    this.getGenres();
    this.getMovies('popular');
    this.getMovies('top_rated');
    this.getMovies('upcoming');
  },
};
</script>

<style>
:root {
  --bgdark: #000;
  --bgdark-transparent: rgba(0, 0, 0, 0.2);
  --black: #211f1f;
  --dark-grey: #292f33;
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
