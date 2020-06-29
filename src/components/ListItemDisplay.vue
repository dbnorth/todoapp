<template>
  <tr>
    <td>
      <span v-if="!editItem">{{ item.name }}</span>
      <input v-model="item.name" type="text" v-if="editItem" />
    </td>
    <td>
      <span v-if="!editItem">{{ item.description }}</span>
      <input v-model="item.description" type="text" v-if="editItem" />
    </td>
    <td>
      <span v-if="!editItem">{{ item.state }}</span>
      <input v-model="item.state" type="text" v-if="editItem" />
    </td>
    <td>
      <button v-if="!editItem" @click="editForm">edit</button>
      <button v-if="editItem" @click="updateItem">save</button>
      <button @click="deleteItem">delete</button>
    </td>
  </tr>
</template>

<script>
export default {
  props: {
    item: Object
  },
  data() {
    return {
      editItem: false
    };
  },
  methods: {
    editForm() {
      this.editItem = true;
    },
    deleteItem() {
      this.$emit("deleteItem");
    },
    updateItem() {
      this.$emit("updateItem");
      this.editItem = false;
    }
  }
};
</script>

<style></style>
