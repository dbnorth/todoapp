<template>
  <span>
    <span v-if="loggedin">
      Welcome, {{ user.firstName }}
      <router-link :to="{ name: 'logoutuser' }">(Logout)</router-link>
    </span>
    <span v-if="!loggedin">No user logged in</span>
  </span>
</template>

<script>
import TodoServices from "@/services/TodoServices.js";
export default {
  data() {
    return { user: {}, loggedin: false };
  },

  created() {
    this.getUser();
  },
  methods: {
    getUser() {
      TodoServices.getUser()
        .then(response => {
          this.user = response.data.user;
          this.loggedin = true;
        })
        .catch(() => {
          this.loggedin = false;
          this.user = null;
          localStorage.setItem("token", "");
        });
    }
  }
};
</script>

<style></style>
