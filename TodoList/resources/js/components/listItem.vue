<template>
    <div class="item">
        <input type="checkbox" @change="updateTodo()" v-model="item.completed">
        <span :class="['itemText', item.completed ? 'completed' : '']">
            {{ item.todo }}
        </span>
        <button class="edit">
            <font-awesome-icon
            icon="edit"
            />
        </button>
        <button class="delete" @click="removeTodo()">
            <font-awesome-icon
            icon="trash"
            />
        </button>
    </div>
</template>

<script>
export default {
    props: ['item'],
    methods: {
        updateTodo() {
            axios.post('api/todos/update/'+this.item.id, {
                completed: this.item.completed
            }).then(response => {
                if(response.status >= 200 && response.status < 300) {
                    alert('Item updated succesfully')
                }
            })
        },

        removeTodo() {
            axios.get('api/todos/delete/'+this.item.id).then(response => {
                if(response.status >= 200 && response.status < 300) {
                    alert('Item deleted succesfully')
                }
            })
        }
    }
}
</script>

<style>
    .item {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .item:hover {
        background-color: aliceblue;
    }

    .completed {
        text-decoration: line-through;
        color: #999999;
    }

    .itemText {
        width: 100%;
        margin-left: 20px;
    }

    .edit {
        color: blue;
        border-radius: 5px;
        border: none;
        outline: none;
        margin-right: 5px;
        background-color: white;
        font-size: 17px;
    }

    /* .edit:hover {
        color: darkblue;
    }

    .edit:active {
        color: darkgreen;
    } */

    .delete {
        color: red;
        border-radius: 5px;
        border: none;
        outline: none;
        margin-right: 5px;
        background-color: white;
        font-size: 17px;
    }

    /* .delete:hover {
        color: darkred;
    }

    .delete:active {
        color: pink;
        background-color: darkred;
    } */

</style>