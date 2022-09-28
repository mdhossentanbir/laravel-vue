<template>
    <div v-for="(item, index) in items" :key="index">
        <Item :item="item" class="item" v-on:itemUpdated="$emit('reloadList')"/>
    </div>
</template>

<script>
import Item from './item.vue'
export default {
    name: "list",
    props: ['items'],
    emits:['reloadList'],
    components:{
        Item
    }
}
</script>

<style scoped>
.item {
    background: #e6e6e6;
    padding: 5px;
    margin-top: 5px;
}
</style>
