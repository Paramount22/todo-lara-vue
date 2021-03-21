<template>
    <div class="todo-list-container">
        <div class="heading">
            <h2  class="title">Todo List</h2>
            <add-item-form v-on:reloadlist="getList" />
        </div>
        <list-view :items="items" v-on:reloadlist="getList"/>

    </div>
</template>

<script>
    import addItemForm from './addItemForm';
    import listView from './listView';
    export default {
        name: "app",
        components: {
            addItemForm,
            listView
        },

        data() {
            return {
                items: []
            }
        },

        methods: {
            getList() {
                axios.get('api/items')
                    .then(response => {
                        // handle success
                        this.items = response.data
                    })
                    .catch( error => {
                        // handle error
                        console.log(error);
                    })
            }
        },
        created() {
            this.getList();
        }

    }
</script>

<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=Nunito:wght@400;600&display=swap');
    * {
        margin: 0;
        padding: 0;
        box-sizing:border-box;
    }

    .todo-list-container {
        width: 350px;
        margin: auto;
        font-family: 'Nunito', sans-serif;
    }

    .heading {

        background: #e6e6e6;
        padding: 10px;
    }
</style>
