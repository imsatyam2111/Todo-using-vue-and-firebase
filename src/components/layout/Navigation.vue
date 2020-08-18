<template>
  <div class="container bg-info">
    <nav class="navbar navbar-expand-lg navbar-dark px-0 px-sm-3 pt-3 pb-3">
      <a class="navbar-brand" href="#">Vue Todo</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div id="nav" class="navbar-nav ml-auto">
          <li v-if="isLoggedIn" class="pr-2">
            <span class="email text-dark">
              {{ currentUser }}
            </span>
          </li>
          <router-link v-if="isLoggedIn" class="mt-3 mt-lg-0 pr-3" to="/">
            Dashboard
          </router-link>
          <router-link v-if="!isLoggedIn" class="mt-3 mt-lg-0 pr-3" to="/login">
            Login
          </router-link>
          <router-link v-if="!isLoggedIn" class="mt-3 mt-lg-0 pr-3" to="/register">
            Register
          </router-link>
          <button
            v-if="isLoggedIn"
            class="logout btn btn-danger mt-3 mt-lg-n2"
            v-on:click="logout"
          >
            Logout
          </button>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import firebase from "firebase";

export default {
  name: "Navigation",
  data() {
    return {
      isLoggedIn: false,
      currentUser: false
    };
  },
  created() {
    if (firebase.auth().currentUser) {
      this.isLoggedIn = true;
      this.currentUser = firebase.auth().currentUser.email;
    }
  },
  methods: {
    logout: function() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.$router.go({ path: this.$router.path });
        });
    }
  }
};
</script>

<style scoped>
  @media (max-width: 769px) {
    .logout {
      margin-left: auto;
      width: 25%;
    }
  }
</style>
