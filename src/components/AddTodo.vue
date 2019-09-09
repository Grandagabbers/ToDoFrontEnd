<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="Add Todo...">
            <input type="submit" name="Submit" class="btn">
        </form>
    </div>
</template>

<script>
export default {
    name: "AddToDo",
    data(){
        return{
            title:''
        }
    },
    methods: {
        addTodo(e){
            e.preventDefault();
            const newTodo = {
               title: this.title,
               completed: false
            }
            // Send up to parent
            this.$emit('add-todo', newTodo);
            this.title = '';
        }
    }
}
</script>

<style scoped>
    form{
    margin-left: auto;
    margin-right: auto;
    display: flex;
    width: 20em;
    }
    input[type="text"]{
        flex: 20;
        padding: 5px;
        width: 500px;
    }
    input[type="Submit"]{
        cursor: pointer;
        background-color: turquoise;
        border: none;
        color: white;
        padding: 20px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        margin: 4px 2px;
        border-radius: 50%      
    }
    input[type="Submit"]:hover{
        color: blue;
        background: color blue;
        cursor: pointer;
    }
</style>