<template>
    <div class="item">
        <input
            type="checkbox"
            @change="updateCheck()"
            :checked="item.completed===1"
            :value="item.completed"
            v-model="item.completed"
        />
        <span :class="[item.completed?'completed':'', 'itemText']">{{ item.name }}</span>
        <button @click="removeItem()" class="trashcan">
            <font-awesome-icon icon="trash"/>
        </button>
    </div>
</template>

<script>
import axios from "axios";

export default {
    name: "item",
    props: ['item'],
    methods: {
        updateCheck() {
            console.log(this.item.completed)
            axios.put('api/item/' + this.item.id, {
                completed: this.item.completed
            }).then(response=>{
                if(response.status ===200){
                    this.$emit.item;
                    this.$emit('itemUpdated');
                }
            }).catch(e=>{
                console.log(e)
            })
        },
        removeItem() {
            axios.delete('api/item/' + this.item.id).then(response=>{
                if(response.status ===200){
                    this.$emit('itemUpdated');
                }
            }).catch(e=>{
                console.log(e)
            })
        }
    }
}
</script>

<style scoped>

.completed {
    text-decoration: line-through;
    color: #999999;
}

.itemText {
    width: 100%;
    margin-left: 20px;
}

.item {
    display: flex;
    justify-content: center;
    align-items: center;
}

.trashcan {
    background: #e6e6e6;
    border: none;
    color: #971010;
    outline: none;
}

</style>
