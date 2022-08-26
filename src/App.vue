<script>
export default {
  data: function () {
    return {
      isLoggedIn: false,
      flashMessage: "",
    };
  },
  watch: {
    $route: function () {
      this.isLoggedIn = !!localStorage.jwt;
      this.flashMessage = localStorage.getItem("flashMessage");
      localStorage.removeItem("flashMessage");
    },
  },
};
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="/">Blg</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link" href="/posts">Posts</a>
          </li>
          <li class="nav-item">
            <a v-if="!isLoggedIn" class="nav-link" href="/signup">Signup</a>
          </li>
          <li class="nav-item">
            <a v-if="!isLoggedIn" class="nav-link" href="/login">Login</a>
          </li>
          <li class="nav-item">
            <a v-if="isLoggedIn" class="nav-link" href="/logout">Logout</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <div v-if="flashMessage" v-on:click="this.flashMessage = ''" class="alert alert-success">{{ flashMessage }}</div>
  <router-view />
</template>

<style>
body,
#app {
  font-family: "Big Caslon", "Book Antiqua", "Palatino Linotype", Georgia, serif;
  background-image: url("./assets/dot-grid.png");
  width: 99vw;
  margin: auto;
  margin-left: -40px;
  padding-left: 40px;
}

nav {
  width: 100vw;
  margin-left: -40px;
}

a {
  color: brown;
}

.smaller {
  font-size: smaller;
}
</style>
