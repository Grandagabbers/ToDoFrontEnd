<template>
    <div>
       <div v-bind:key="todo.id" v-for="todo in todos">
           <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" v-on:up-todo="$emit('up-todo', todo.id)" v-on:change-todo="$emit('change-todo', todo.id)"/>
        </div>
    </div>
</template>

<script>
import TodoItem from './TodoItem.vue'

export default {
    name: "Todos",
    components:{
        TodoItem
    },
    props: ["todos"]
}
</script>

><style scoped>

</style>