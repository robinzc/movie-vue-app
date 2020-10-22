<template>
  <div class="movies-index">
    <h2>All Movies</h2>
    <div class="row mb-3 mt-3">
      <input
        type="text"
        v-model="titleFilter"
        placeholder="Search by title"
        list="titles"
      />
      <datalist id="titles">
        <option v-for="movie in movies">{{ movie.title }}</option>
      </datalist>
      <div>
        <button v-on:click="setSortAttribute('title')">
          Sort Alphabetically
        </button>
      </div>
      <div
        v-for="movie in orderBy(
          filterBy(movies, titleFilter, 'title'),
          'title'
        )"
      ></div>
      <div>
        <div class="card">
          <div v-for="movie in filterBy(movies, titleFilter, 'title', 'plot')">
            <router-link :to="`/movies/${movie.id}`"> </router-link>
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
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      titleFilter: "",
      sortAttribute: "title,",
    };
  },
  created: function() {
    axios.get("/api/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {
    setSortAttribute: function(attribute) {
      this.sortAttribute = attribute;
    },
  },
};
</script>
