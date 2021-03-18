<template>
  <div class="container py-5" id="movie-details">
    <div class="row justify-content-center">
      <div class="col-md-3" id="img-container">
        <img :src="imgUrl" class="img-fluid" :alt="movie.title" />
      </div>
      <div class="col-md-6 d-flex flex-column justify-content-between">
        <div class="ranking">
          <i class="fas fa-star"></i>
          <h5>{{ movie.vote_average }}</h5>
          <span>/10</span>
        </div>
        <h5 class="title">{{ movie.title }}</h5>
        <p class="date">Release date: 2{{ movie.release_date }}</p>
        <p class="text">
          {{ movie.overview }}
        </p>
        <div class="genre-container d-flex mb-2">
          <GenreBtn
            v-for="(genre, index) in genreNames"
            :key="index"
            :genre="genre"
          />
        </div>
        <div class="d-flex">
          <a :href="url" target="_blank">
            <button class="btn btn-danger mr-2 mb-1">
              <i class="fas fa-external-link-alt mr-2"></i>Rotten Tomatoes
            </button>
          </a>
          <a href="#" target="_blank">
            <button @click.prevent="searchSimilar" class="btn btn-danger mb-1">
              <i class="fab fa-mixer pr-2"></i>View recommended
            </button>
          </a>
        </div>
      </div>
      <div class="col-md-5"></div>
    </div>
  </div>
</template>

<script>
import GenreBtn from './GenreBtn.vue';

export default {
  name: 'MovieDetails',
  components: { GenreBtn },
  props: {
    movie: {
      type: Object,
      required: true,
    },
    genreNames: {
      type: Array,
      required: true,
    },
  },
  computed: {
    imgUrl() {
      let path = `https://image.tmdb.org/t/p/w500${this.movie.poster_path}`;
      return path;
    },
  },
  data() {
    return {
      url: '',
    };
  },
  methods: {
    searchSimilar() {
      this.$emit('searchSimilar', this.movie.id, this.movie.title);
    },
    modifyTitle(str, sep) {
      const stringArr = str.toLowerCase().split(sep);
      return stringArr.join('_');
    },
    createLink(title) {
      return `https://www.rottentomatoes.com/m/${title}`;
    },
  },

  mounted() {
    const space = ' ';
    const title = this.modifyTitle(this.movie.title, space);
    return (this.url = this.createLink(title));
  },
};
</script>

<style scoped>
.ranking {
  display: flex;
  margin-bottom: -10px;
  font-size: 1.5rem;
}
.fa-star {
  color: #e4bb24;
  margin-right: 0.3rem;
  margin-top: 0.2rem;
}
.ranking h5 {
  font-weight: 400;
  margin: 0.3rem;
}
span {
  color: var(--grey);
  margin-top: 0.8rem;
  font-size: 0.7rem;
}
.title {
  color: var(--white);
  text-transform: uppercase;
  font-weight: 600;
  font-size: 2rem;
}
.date {
  font-size: 0.8rem;
  margin-top: -1rem;
}
a {
  text-decoration: none;
}
</style>
