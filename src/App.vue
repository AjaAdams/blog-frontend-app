<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/test">Test</router-link> |
      <router-link to="/signup">Sign Up</router-link> |
      <router-link to="/postsindex">Post Index</router-link> |
      <router-link to="/posts/new">New Post</router-link> |
      <router-link to="/login">Login</router-link> |
      <router-link to="/posts/:id">Show Post</router-link>

    </div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="/postsindex">Navbar</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav">
      <li class="nav-item active">
        <a class="nav-link" href="/postsindex">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="/posts/new">New Post</a>
      </li>
      <li v-if="!isLoggedIn()"class="nav-item">
        <a class="nav-link" href="/login">Login</a>
      </li>
      <li v-if="isLoggedIn()"class="nav-item">
        <a class="nav-link" href="/logout">Logout</a>
      </li>
      <li v-if="!isLoggedIn()"class="nav-item">
        <a class="nav-link" href="/signup">Sign Up</a>
      </li>
    </ul>
  </div>
</nav>

<div class="alert alert-success" v-if="flashMessage" v-on:click="flashMessage=''">
  {{ flashMessage }}
</div>
    <router-view/>
  </div>
</template>

<style>
body {
  font-family: Papyrus, fantasy;
  background-image: url("./assets/bg.jpg");
}
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
} */
</style>

<script>
export default {
  data: function() {
    return {
      flashMessage: ""
    }
  },
  methods: {
    isLoggedIn: function() {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserId: function() {
      return localStorage.getItem("user_id");
    }
  }
};
</script>
