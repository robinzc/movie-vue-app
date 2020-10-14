
<template>
  <div class="home">
    <div>
      <h2>New Movie</h2>
      <p>Title <input type="text" v-model="newMovieTitle"> </p>
      <p>Year <input type="text" v-model="newMovieYear"></p>
      <p>Plot <input type="text" v-model="newMoviePlot"></p>
      <p>Director <input type="text" v-model="newMovieDirector"></p>
      <p>English <input type="text" v-model="newMovieEnglish"></p>
      <button v-on:click="createMovie">Create movie</button>
    </div>
    <h1>Movies!</h1>
    <div v-for="movie in movies">
      <h2>Title: {{ movie.title }}</h2>
      <h4>Year: {{ movie.year }}</h4>
      <h4>Plot: {{ movie.plot }}</h4>
      <h4>Director: {{ movie.director }}</h4>
      <h5>English: {{ movie.english }}</h5>
      <button v-on:click="showMovie(movie)">More Info</button>
    </div>

    <dialog id="movie-details">
      <form method="dialog">
        <h2>Movie Info</h2>
        <p>Title <input type="text" v-model="currentMovie.title"></p>
        <p>Year <input type="text" v-model="currentMovie.year"></p>
        <p>Plot <input type="text" v-model="currentMovie.plot"></p>
        <p>Director <input type="text" v-model="currentMovie.director"></p>
        <p>English <input type="text" v-model="currentMovie.english"></p>
        <button v-on:click="updateMovie(currentMovie)">Update Movie</button>
        <button v-on:click="destroyMovie(currentMovie)">Destroy Movie</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieEnglish: "",
      currentMovie: {}
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios.get("/api/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
        english: this.newMovieEnglish,
      };

      axios.post("/api/movies", params).then((response) => {
        console.log("Success", response.data);
      })
        .catch((error) => {
          console.log(error.response);
        });
    },
    showMovie: function(movie) {
      console.log(movie.title);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function(movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director,
        english: movie.english,
      };
      axios.patch(`/api/movies/${movie.id}`, params).then(response => {
        console.log("Success", response.data);
      })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    },
    destroyMovie: function(movie) {
      axios.delete(`/api/movies/${movie.id}`).then(response => {
        console.log("Success", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    }
  }
};
</script>

