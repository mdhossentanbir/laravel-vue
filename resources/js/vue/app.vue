<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <AddForm v-on:reloadList="getItems()"/>
        </div>
        <List :items="items" v-on:reloadList="getItems()"/>

    </div>
</template>

<script>
import AddForm from './addForm.vue'
import List from './list.vue'
import axios from "axios";

export default {
    components: {
        AddForm,
        List
    },
    data: function () {
        return {
            items: []
        }
    },
    methods: {
        getItems() {
            axios.get('api/items')
                .then(response => {
                    this.items = response.data
                }).catch(e => {
                console.log(e);
            })
        }
    },
    created() {
        this.getItems()
    }
}
</script>

<style scoped>
.todoListContainer {
    width: 350px;
    margin: auto;
}

.heading {
    background: #e6e6e6;
    padding: 10px;
}

#title {
    text-align: center;
}
</style>

