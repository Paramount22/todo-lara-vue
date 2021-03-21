<template>
    <div class="add-item">
        <form class="add-form" @submit.prevent="addItem">
            <label for="add"> </label>
                <input type="text"  id="add" v-model="item.name"/>
            <i class="fas fa-plus-square"
               :class="[item.name ? 'active' : 'inactive', 'plus' ]"
               @click="addItem"
            >
            </i>
        </form>

    </div>
</template>

<script>
    export default {
        name: "addItemForm",
        data() {
            return {
                item: {
                    name: ''
                }
            }
        },

        methods: {
            addItem() {
                if( !this.item.name ) return;
                axios.post('api/item/store', {
                    item: this.item
                }).then( response => {
                        if(response.status === 201 ) {
                            this.item.name = '';
                            this.$emit('reloadlist')
                        }
                    })
                    .catch( error => {
                        console.log(error);
                    })
            }
        }
    }
</script>

<style scoped>
    .add-item {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .add-form {
        width: 100%;
    }
    input {
        background: #f7f7f7;
        border: none;
        outline:none;
        padding: 5px;
        border-radius: 3px;
        width: 85%;
    }
    .plus {
        font-size: 30px;
        position: relative;
        top: 6px;
        cursor: pointer;
    }

    .active {
        color: #00ce25;
    }
    .inactive {
        color: #999999;
    }
</style>
