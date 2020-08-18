<template>
  <div id="app" class="container-info">
    <div class="nav bg-info">
      <Navigation />
    </div>
    <router-view />
  </div>
</template>

<script>
import Navigation from "@/components/layout/Navigation.vue";
export default {
  components: {
    Navigation
  }
};
</script>

<style>
body {
  background: #e3e3e9;
}
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
