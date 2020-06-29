<template>
  <div>
    <H1>Todo Add User</H1>

    <form @submit.prevent="addUser">
      First name:
      <input v-model="user.firstName" type="text" id="firstName" />
      <br />Last name:
      <input v-model="user.lastName" type="text" id="lastName" />
      <br />Username:
      <input v-model="user.username" type="text" id="username" />
      <br />Password:
      <input v-model="user.password" type="text" id="password" />
      <br />
      <input type="submit" name="submit" value="Save" />
      <button name="cancel" v-on:click.prevent="cancel()">Cancel</button>
    </form>
  </div>
</template>

<script>
import TodoServices from "@/services/TodoServices.js";

export default {
  data() {
    return {
      user: {}
    };
  },

  methods: {
    addUser() {
      TodoServices.addUser(this.user)
        .then(() => {
          this.$router.push({ name: "list" });
        })
        .catch(error => {
          console.log(error);
        });
    },
    cancel() {
      this.$router.push({ name: "list" });
    }
  }
};
</script>

<style scoped></style>
