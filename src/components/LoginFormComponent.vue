<template>
  <div class="w-full max-w-md">
    <form name="form" @submit.prevent="handleLogin" class="login-form">
      <h1 class="title">Welcome Player</h1>
      <div class="mb-4">
        <span class="input-label">Username</span>
        <input
          type="text"
          class="form-control"
          name="username"
          placeholder="Username"
          id="username"
          v-model="user.username"
        />
        <div v-if="this.usernameMissing" role="alert">
          <p class="error">Please choose an username!</p>
        </div>
      </div>
      <div class="mb-4">
        <input
          type="password"
          class="form-control "
          name="password"
          placeholder="Password"
          v-model="user.password"
          id="password"
        />
        <div v-if="this.passwordMissing" role="alert">
          <p class="error">Please choose a password!</p>
        </div>
      </div>
      <div class="flex justify-between">
        <button class="login-btn btn-unstyled" type="submit" id="submit">
          Sign In
        </button>
      </div>
      <div class="form-group">
        <div v-if="message" class="error" role="alert">
          <br />
          {{ message }}
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import User from "@/models/user";

export default {
  name: "Login",
  data() {
    return {
      user: new User("", ""),
      message: "",
      usernameMissing: false,
      passwordMissing: false,
    };
  },
  computed: {
    loggedIn() {
      return this.$store.state.auth.status.loggedIn;
    },
  },
  created() {
    if (this.loggedIn) {
      //this.$router.push("/");
    }
  },
  methods: {
    handleLogin: function(e) {
      if (this.user.username == "") {
        this.usernameMissing = true;
      }
      if (!this.user.password) {
        this.passwordMissing = true;
      }

      if (this.user.username && this.user.password) {
        this.usernameMissing = false;
        this.passwordMissing = false;
        this.$store.dispatch("auth/login", this.user).then(
          () => {
            this.$router.push("/");
          },
          (error) => {
            if (error.response.data.title == "Unauthorized") {
              this.message =
                "Incorrect username or password, please try agian.";
            } else {
              this.message =
                "Incorrect username or password, please try again.";
              // remove later //
              console.log(
                (error.response && error.response.data) ||
                  error.message ||
                  error.toString()
              );
            }
          }
        );
      }
      e.preventDefault();
    },
  },
};
</script>

<style lang="css" scoped>
.input-label {
  font-size: 17px;
}
.title {
  text-align: center !important;
  margin-top: 0px;
  font-family: "Rubik One", Helvetica, Arial;
  text-align: left;
  font-size: 21px;
}
.login-form {
  font-family: "Montserrat Alternates", Helvetica, Arial;
  background-color: #e3daca;
  padding: 2em;
  border-radius: 24px;
  box-shadow: inset 0px 0px 32px #807c74;
}
.form-control {
  background-color: rgba(1, 1, 1, 0);
  color: #907604;
  border: none;
  border-radius: 0px;
  box-shadow: none;
  border-bottom: 3px solid #907604;
  margin-bottom: 1em;
  padding: 0em;
}

.error {
  color: crimson;
  font-size: 11px;
}

.login-btn {
  background-color: rgba(1, 1, 1, 0);
  box-shadow: none;
  border: none;
  width: auto;
  font-size: 17px;
  font-weight: 700;
  display: inline-block;
}
</style>
