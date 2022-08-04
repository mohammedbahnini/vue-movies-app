<template>
  <div class="movies" :class="{ fill: movies.length > 0 }">
    <MoviesLoader v-if="loading" />
    <slot v-else>
      <MovieItem
        v-for="(movie, index) in movies"
        :movie="movie"
        :index="index"
      />
    </slot>
  </div>
</template>

<script>
import MovieItem from "./MovieItem.vue";
import MoviesLoader from "./MoviesLoader.vue";

export default {
  props: ["movies", "loading"],
  methods: {},
  components: {
    MovieItem,
    MoviesLoader,
  },
  mounted() {
    //this.getMovies();
    console.log(this.loading);
  },
};
</script>
