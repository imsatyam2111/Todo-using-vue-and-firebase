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
          <router-link class="pr-3" to="/">Home</router-link>
          <router-link class="pr-3" to="/login">Login</router-link>
          <router-link class="pr-3" to="/register">Register</router-link>
        </div>
      </div>
    </nav>
  </div>
</template>
