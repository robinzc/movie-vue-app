<template>
  <div class="movies-show">


      <h2>{{ movie.title }}</h2>
      <p>{{ movie.year }}</p>
      <p>{{ movie.plot }}</p>
      <p>Director: {{ movie.director }} </p>
      <p>English: {{ movie.english }} </p>
      <router-link :to="`/movies/${movie.id}/edit`">Edit Movie</router-link>

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {}
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {}
};
</script>