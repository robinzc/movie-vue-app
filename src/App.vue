<template>
  <div id="app">
    <div id="nav">
      <nav class="navbar navbar-dark bg-dark">
        <a class="navbar-brand" href="#">Movies</a>
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
              <a class="nav-link"></a>
              <router-link to="/">Home</router-link>
            </li>
            <li class="nav-item" v-if="!isLoggedIn()">
              <a class="nav-link"></a>
              <router-link to="/signup">Signup</router-link>
            </li>
            <li class="nav-item" v-if="!isLoggedIn()">
              <a class="nav-link"></a>
              <router-link to="/login">Login</router-link>
            </li>
            <li class="nav-item">
              <a class="nav-link"></a>
              <router-link to="/movies">Movies</router-link>
            </li>
            <li class="nav-item">
              <a class="nav-link"></a>
              <router-link to="/movies/new">New Movie</router-link>
            </li>
            <li class="nav-item" v-if="isLoggedIn()">
              <a class="nav-link"></a>
              <router-link to="/logout">Logout</router-link>
            </li>
          </ul>
          <form class="form-inline my-2 my-lg-0">
            <input
              class="form-control mr-sm-2"
              type="search"
              placeholder="Search"
              aria-label="Search"
            />
            <button class="btn btn-outline-success my-2 my-sm-0" type="submit">
              Search
            </button>
          </form>
        </div>
      </nav>
    </div>
    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      // flashMessage: "",
    };
  },
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    },
    getUserId: function() {
      return localStorage.getItem("user_id");
    },
  },
};
</script>
