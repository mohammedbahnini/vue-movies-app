<template>
  <div
    class="movie"
    :style="{ transitionDelay: `${index * 0.05}s` }"
    ref="movieSection"
  >
    <div class="movie__poster">
      <img
        :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
        :alt="movie.title"
      />
    </div>
    <div class="movie__info">
      <p class="title">{{ movie.title }}</p>
      <span class="rating" :class="classRating()">
        {{ movie.vote_average.toFixed(1) }}</span
      >
    </div>
    <div class="movie__overview">
      <h3 class="movie__overview-title">Overview</h3>
      <p>{{ movie.overview }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["movie", "index"],
  methods: {
    classRating() {
      if (this.movie.vote_average >= 8) return "green";
      else if (this.movie.vote_average >= 5) return "orange";
      else return "red";
    },
  },
  data() {
    return {
      isVisible: false,
    };
  },
  mounted() {
    setTimeout(() => {
      this.isVisible = true;
    }, 20);

    const obersever = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add("visible");
        }
        console.log(entry.isIntersecting);
      });
    });
    obersever.observe(this.$refs.movieSection);
  },
};
</script>
