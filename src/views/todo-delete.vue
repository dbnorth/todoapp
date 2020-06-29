<template>
  <div>
    <H1>Todo List Delete</H1>
    <h4>Delete {{ list.name }} ?</h4>
    <button v-on:click="deleteToDoList()">Delete</button>
    <button v-on:click="cancel()">Cancel</button>
  </div>
</template>

<script>
import TodoServices from "@/services/TodoServices.js";
export default {
  props: ["id"],

  data() {
    return {
      list: Object
    };
  },
  created() {
    TodoServices.getList(this.id)
      .then(response => {
        this.list = response.data.list;
        console.log(this.list);
      })
      .catch(error => {
        console.log("There was an error:", error.response);
      });
  },

  methods: {
    deleteToDoList() {
      TodoServices.deleteList(this.id)
        .then(response => {
          this.$router.push({ name: "list" });
          console.log(response);
        })
        .catch(error => {
          console.log(error.data);
        });
    },
    cancel() {
      this.$router.push({ name: "list" });
    }
  }
};
</script>

<style></style>
