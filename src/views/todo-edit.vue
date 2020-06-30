<template>
    <div>
        <UserDisplay></UserDisplay>
        <H1>Todo List Edit</H1>
        <p>{{ message }}</p>
        <h2>Editing {{ this.list.name }}</h2>
        <form @submit.prevent="updateList">
            Name:
            <input v-model="list.name" type="text" id="id" />
            <input type="submit" name="submit" value="Save" />
            <button name="cancel" v-on:click.prevent="cancel()">Cancel</button>
        </form>
        <button name="add" v-on:click.prevent="addForm()">Add Item</button>

        <table class="center">
            <ListItemDisplay
                v-for="item in items"
                :key="item.id"
                :item="item"
                @deleteItem="deleteItem(item.id)"
                @updateItem="updateItem(item)"
            />
            <ListItemAdd v-if="addItemDisplay" @addItem="addItem" />
        </table>
    </div>
</template>

<script>
import TodoServices from '@/services/TodoServices.js';
import UserDisplay from '@/components/UserDisplay.vue';
import ListItemDisplay from '@/components/ListItemDisplay.vue';
import ListItemAdd from '@/components/ListItemAdd.vue';

export default {
    props: ['id'],
    components: {
        UserDisplay,
        ListItemDisplay,
        ListItemAdd,
    },
    data() {
        return {
            list: {},
            items: {},
            message: 'Make updates to the List',
            addItemDisplay: false,
        };
    },
    created() {
        TodoServices.getList(this.id)
            .then(response => {
                this.list = response.data.list;
            })
            .catch(error => {
                console.log('There was an error:', error.response);
            });
        TodoServices.getListItems(this.id)
            .then(response => {
                this.items = response.data.items;
            })
            .catch(error => {
                console.log('There was an error:', error.response);
            });
    },

    methods: {
        addForm() {
            this.addItemDisplay = true;
        },
        updateList() {
            TodoServices.updateList(this.id, this.list)
                .then(() => {
                    this.$router.push({ name: 'list' });
                })
                .catch(error => {
                    this.message = error.response.data.message;
                });
        },
        addItem(item) {
            TodoServices.addListItem(this.id, item)
                .then(response => {
                    item.id = response.data.itemId;
                    this.message = 'Added Item';
                    this.items.push(item);
                    this.addItemDisplay = false;
                })
                .catch(error => {
                    this.message = error.response.data.message;
                });
        },
        cancel() {
            this.$router.push({ name: 'list' });
        },
        updateItem(item) {
            TodoServices.updateListItem(this.id, item.id, item).catch(error => {
                this.message = error.data.message;
            });
        },
        deleteItem(id) {
            TodoServices.deleteListItem(this.id, id)
                .then(() => {
                    //     this.items = this.items.filter(item => item.id != id)
                    this.items.forEach((item, i) => {
                        if (item.id == id) {
                            this.items.splice(i, 1);
                        }
                    });
                })
                .catch(error => {
                    this.message = error.response.data.message;
                });
        },
    },
};
</script>

<style>
table,
th,
td {
    border: 1px solid black;
    text-align: 'left';
}
table.center {
    width: 70%;
    margin-left: 15%;
    margin-right: 15%;
    border-collapse: collapse;
}
</style>
