<template>
  <tr>
    <td>
      <input type="text" v-model="item.name" />
    </td>
    <td>
      <input type="text" v-model="item.description" />
    </td>
    <td>
      <input type="text" v-model="item.state" />
    </td>

    <td>
      <button @click="addItem">
        <span>Save</span>
      </button>
    </td>
  </tr>
</template>

<script>
export default {
  data() {
    return { item: {} };
  },
  methods: {
    addItem() {
      this.$emit("addItem", this.item);
    }
  }
};
</script>

<style></style>
