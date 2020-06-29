<template>
  <div>
    <H1>Todo List Add</H1>

    <form @submit.prevent="addToDoList">
      Name:
      <input v-model="list.name" type="text" id="id" />
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
      list: {}
    };
  },

  methods: {
    addToDoList() {
      TodoServices.addList(this.list)
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
