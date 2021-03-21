<template>
    <ul >
        <list-item v-for="(item, index) in items"
                   :key="index" :item="item"
                   class="item"
                   v-on:itemChanged="$emit('reloadlist')"
        />
    </ul>
</template>

<script>
    import listItem from './listItem'
    export default {
        name: "listView",
        props: ['items'],
        components: {
            listItem
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
