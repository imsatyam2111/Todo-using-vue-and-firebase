<template>
  <div id="register">
    <h3 class="text-center text-white pt-5">register form</h3>
    <div class="container">
      <div
        id="register-row"
        class="row justify-content-center align-items-center"
      >
        <div id="register-column" class="col-md-6">
          <div id="register-box" class="col-md-12">
            <form id="register-form" class="form" action="" method="post">
              <h3 class="text-center text-info">Register</h3>
              <div class="form-group">
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
              <div class="form-group">
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
              <div class="form-group">
                <button
                  type="submit"
                  class="btn btn-info w-100"
                  v-on:click="register"
                >
                  Register
                </button>
              </div>
              <div id="register-link" class="text-center">
                <router-link to="/login" class="text-info">
                  Login here
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
    register: function(e) {
      firebase
        .auth()
        .createUserWithEmailAndPassword(this.email, this.password)
        .then(user => {
          console.log(user)
          alert(`Account created for ${user.user.email}`);
          this.$router.push("/");
        })
        .catch(err => alert(err));

      e.preventDefault();
    }
  }
};
</script>

<style scoped>
body {
  margin: 0;
  padding: 0;
  background-color: #17a2b8;
}
#register-box {
  max-width: 600px;
  border: 1px solid #9c9c9c;
  background-color: #eaeaea;
}
#register
  .container
  #register-row
  #register-column
  #register-box
  #register-form {
  padding: 20px;
}
</style>
