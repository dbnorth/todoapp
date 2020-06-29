<template>
  <div>
    <H1>Todo Logout</H1>
    <p>{{ this.message }}</p>
    <h4>Logout {{ user.firstName }} {{ user.lastName }} ?</h4>
    <button v-on:click="logout()">Logout</button>
    <button v-on:click="cancel()">Cancel</button>
  </div>
</template>

<script>
import TodoServices from "@/services/TodoServices.js";
export default {
  props: ["id"],
  data() {
    return {
      user: Object,
      message: "Click to Logout"
    };
  },
  created() {
    TodoServices.getUser(this.id)
      .then(response => {
        this.user = response.data.user;
        console.log(this.user);
      })
      .catch(error => {
        console.log("There was an error:", error.response);
      });
  },

  methods: {
    logout() {
      TodoServices.logoutUser(this.user)
        .then(response => {
          localStorage.setItem("token", "");
          this.$router.push({ name: "list" });
          console.log(response);
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

<style></style>
