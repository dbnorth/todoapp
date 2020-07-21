<template>
    <div>
        <UserDisplay></UserDisplay>
        <H1>ToDo List</H1>
        <p>{{ message }}</p>
        <ToDoListDisplay v-for="todolist in todolists" :key="todolist.id" :todolist="todolist" />
    </div>
</template>

<script>
import ToDoListDisplay from '@/components/ToDoListDisplay.vue';
import UserDisplay from '@/components/UserDisplay.vue';
import TodoServices from '@/services/TodoServices.js';

export default {
    components: {
        ToDoListDisplay,
        UserDisplay,
    },
    data() {
        return {
            todolists: [],
            message: '',
        };
    },
    created() {
        TodoServices.getLists()
            .then(response => {
                this.todolists = response.data.lists;
            })
            .catch(error => {
                this.message = error.response.data.message;
            });
    },
};
</script>

<style></style>
