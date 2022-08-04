<template>
  <Header @search="searchMovies" />
  <div class="container">
    <MoviesList :movies="movies" :loading="loading" />
  </div>
</template>

<script>
import Header from "./components/header/Header.vue";
import MoviesList from "./components/movies/MoviesList.vue";
import MoviesLoader from "./components/movies/MoviesLoader.vue";

export default {
  components: {
    Header,
    MoviesList,
    MoviesLoader,
  },
  data() {
    return {
      loading: true,
      movies: [],
    };
  },
  methods: {
    getMovies() {
      setTimeout(async () => {
        const response = await fetch(
          "https://api.themoviedb.org/3/discover/movie?api_key=6f321c0ad255845c8fe32cccd1d01f5f&page=1",
          {
            method: "GET",
          }
        );
        const { results } = await response.json();
        this.movies = results;
        this.loading = false;
      }, 1500);
    },
    searchMovies(movieName) {
      this.loading = true;

      setTimeout(async () => {
        const response = await fetch(
          `https://api.themoviedb.org/3/search/movie?api_key=6f321c0ad255845c8fe32cccd1d01f5f&page=1&include_adult=false&query=${movieName}`,
          {
            method: "GET",
          }
        );
        const { results } = await response.json();
        this.movies = results;
        this.loading = false;
      }, 1500);
    },
  },
  mounted() {
    this.getMovies();
  },
};
</script>
