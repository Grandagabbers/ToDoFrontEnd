<template>
    <div class= "todo-item" v-bind:class="{'is-complete':todo.done}">
        <p>
            <input class="checkbox" type="checkbox" v-on:change="markComplete">
            {{todo.task}}
            <button @click="$emit('del-todo', todo.id)" class="del"> x </button>
        </p>
        <form @submit="changeTodo">
            <input type="text" v-model="title" name="title" placeholder="Update Todo">
            <button class="change" v-on:change-todo="changeTodo" @click="$emit('change-todo', todo.title)"> Update this ToDo </button>        
        </form>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo"],
    data(){
        return{
            title:''
        }
    },
    methods:{
        markComplete(){
            this.$emit('up-todo', this.todo.id)
            this.todo.done = !this.todo.done;
        },
        changeTodo(e){
            e.preventDefault();
            console.log("hallo")
            const changetodo = {
                title: "poehee",
                completed: this.completed
            }
            // Send up to parent
            this.$emit('change-todo', changetodo);
            this.title = '';
        }
        
    }
}
</script>

<style scoped>
    .todo-item{
        background: #fff;
        padding: 25px;
        border-bottom: 1px #ccc dotted;
        color: black;
        text-align: center;
        width: 20em;
        margin-left: auto;
        margin-right: auto;
        display: flex;
    }
    .is-complete{
        text-decoration: line-through;
        color: lightgray;
    }
    .del{
        background: turquoise;
        color: #fff;
        border: none;
        padding: 5px 9px;
        border-radius:50%;
        cursor: pointer;
    }
    .del:hover{
        background: blue;
        color: white;
    }
    .change{
        color: white;
        background-color: turquoise;
        border: 1px solid blue;
        width: 10em;
        cursor: pointer;
    }
    .change:hover{
        color: blue;
        background-color: turquoise;
    }
</style>