<template>
  <div>
    <H1>Todo Login</H1>
    <p>{{ message }}</p>
    <form @submit.prevent="login">
      Username:
      <input v-model="user.username" type="text" id="username" />
      <br />Password:
      <input v-model="user.password" type="text" id="password" />
      <br />
      <input type="submit" name="submit" value="Login" />
      <button name="cancel" v-on:click.prevent="cancel()">Cancel</button>
    </form>
  </div>
</template>

<script>
import TodoServices from "@/services/TodoServices.js";

export default {
  data() {
    return {
      user: {},
      message: "Enter username and password"
    };
  },

  methods: {
    login() {
      TodoServices.loginUser(this.user)
        .then(response => {
          localStorage.setItem("token", response.data.token);
          this.$router.push({ name: "list" });
        })
        .catch(error => {
          this.message = error.response.data.message;
        });
    },
    cancel() {
      this.$router.push({ name: "list" });
    }
  }
};
</script>

<style scoped></style>
