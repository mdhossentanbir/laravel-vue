<template>
    <div class="addItem">
        <input type="text" v-model="name"/>
        <font-awesome-icon
            icon="plus-square"
            @click="addItem()"
            :class="[name?'active':'inactive', 'plus']"
        />
    </div>
</template>

<script>
import axios from "axios";

export default {
    name: "addForm",
    emits:['reloadList'],
    data: function () {
        return {name: ''}
    },
    methods: {
        addItem() {
            if (this.name === '') {
                return;
            }
            axios.post('api/item/store', {
                name: this.name
            }).then(response => {
                if (response.status === 201) {
                    this.name = "";
                    this.$emit('reloadList')
                }
            })
        }
    }
}
</script>

<style scoped>
.addItem {
    display: flex;
    justify-content: center;
    align-items: center;
}

input {
    background: #f7f7f7;
    border: 0;
    outline: none;
    padding: 5px;
    margin-right: 10px;
    width: 100%;
}

.plus {
    font-size: 20px;
}

.active {
    color: #00ce25;
}

.inactive {
    color: #999;
}
</style>
