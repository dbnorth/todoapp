<template>
  <div>
    <span>{{ todolist.name }} {{ todolist.description }} (</span>
    <router-link :to="{ name: 'edit', params: { id: todolist.id } }">
      <span>edit</span>
    </router-link>
    <span>|</span>
    <router-link :to="{ name: 'delete', params: { id: todolist.id } }">
      <span>delete</span>
    </router-link>
    <span>)</span>
  </div>
</template>

<script>
export default {
  props: {
    todolist: Object
  }
};
</script>

<style></style>
