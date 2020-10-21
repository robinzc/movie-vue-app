<template>
  <div class="movies-index">
    <h2>All Movies</h2>
      <div class="card-columns">
        <div v-for="movie in movies">
          <router-link :to="`/movies/${movie.id}`">
          </router-link>
        <div class="card-body">
          <h3 class="card-title">{{ movie.title }}</h3>
          <p class="card-text">{{ movie.year }}</p>
          <p class="card-text">{{ movie.plot }}</p>
          <p class="card-text">Director: {{ movie.director }}</p>
          <router-link :to="`/movies/${movie.id}`">More Info</router-link>
        </div>
        </div>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movies: []
    };
  },
  created: function() {
    axios.get("/api/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {}
};
</script>