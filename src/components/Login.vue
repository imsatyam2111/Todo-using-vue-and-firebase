<template>
  <div id="login">
    <div class="container pt-5">
      <div id="login-row" class="row justify-content-center align-items-center mt-5">
        <div id="login-column" class="col-md-6">
          <div id="login-box" class="col-md-12">
            <form id="login-form" class="form p-4" action="" method="post">
              <h3 class="text-center text-info">Login</h3>
              <div class="form-group text-left mt-5">
                <label for="username" class="text-info">Username:</label><br />
                <input
                  type="email"
                  name="username"
                  id="username"
                  class="form-control"
                  v-model="email"
                  required
                />
              </div>
              <div class="form-group text-left">
                <label for="password" class="text-info">Password:</label><br />
                <input
                  type="password"
                  name="password"
                  id="password"
                  class="form-control"
                  v-model="password"
                  required
                />
              </div>
              <div class="form-group mt-5">
                <button
                  type="submit"
                  class="btn btn-info w-100"
                  v-on:click="login"
                >
                  Login
                </button>
              </div>
              <div id="register-link" class="text-center">
                <router-link to="/register" class="text-info">
                  Register here
                </router-link>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import firebase from "firebase";

export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    login: function(e) {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(user => {
          alert(`Logged in as ${user.user.email}`);
          this.$router.go({ path: this.$router.path });
        })
        .catch(err => alert(err));

      e.preventDefault();
    }
  }
};
</script>

<style scoped>
#login-box {
  max-width: 600px;
  border: 1px solid #9c9c9c;
  background-color: #eaeaea;
}
</style>
