<template>
    <li class="item">
        <input type="checkbox"
            @change="updateCheck"
            v-model="item.completed"
        >
        <span :class="[item.completed ? 'completed' : '', 'item-text']">
          {{ item.name }}
      </span>
        <button @click="removeItem" class="trash">
            <i class="fas fa-trash"></i>
        </button>
    </li>
</template>

<script>
    export default {
        name: "listItem",
        props: ['item'],
        methods: {
            updateCheck() {
                axios.put('api/item/' + this.item.id, {
                    item: this.item
                })
                .then(response => {
                    if(response.status === 200) {
                        this.$emit('itemChanged')
                    }
                })
                    .catch( error => {
                        console.log(error)
                    })
            },

            removeItem() {
                axios.delete('api/item/' + this.item.id)
                    .then( response => {
                        if(response.status === 200) {
                            this.$emit('itemChanged')
                        }
                    })
                    .catch( error => {
                        console.log(error)
                    })
            }
        }
    }
</script>

<style scoped>
    .completed {
        opacity: .3;
        text-decoration: line-through;
    }

    .item {
        display: flex;
        justify-content: center;
        align-items: center
    }

    .item-text {
        width:100%;
        margin-left: 20px;
    }

    .trash {
        background: #e6e6e6;
        border: none;
        color: #ff0000;
        outline: none;
        cursor: pointer;
    }
</style>
