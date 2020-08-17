<template>
  <div id="app container">
    <Navigation />
    <router-view />
  </div>
</template>

<script>
import Navigation from "@/components/layout/Navigation.vue"
export default {
  components: {
    Navigation
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav a {
  font-weight: bold;
  color: #2c3e50;
}
#nav a.router-link-exact-active {
  color: #000;
}
</style>
