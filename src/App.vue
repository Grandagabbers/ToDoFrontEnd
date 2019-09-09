<template>
  <div id="app">
        <Header />
        <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos= "todos" v-on:del-todo="deleteTodo" v-on:up-todo="upTodo" v-on:change-todo="changeTodo"/>
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    AddTodo,
  },
  data(){
      return {
      todos: [
          
      ]
    }
  },
  methods:{
    changeTodo(changetodo){
      const { title, completed } = changetodo;
      axios.put('/todos/change', {
        task: title,
        done: completed,
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(err => console.log(err))
    },
    upTodo(id){
      const upId = this.todos.filter(todo => todo.id === id)
      axios.put(`/todos/update`,
      upId[0],
      )

      .then(res => console.log(res))
      .catch(err => console.log(err))
    },
    deleteTodo(id){
      axios.delete(`/todos/delete`)
        .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err => console.log(err)); 

    },
    addTodo(newTodo){
      const { title, completed } = newTodo;
      axios.post('/todos/post', {
        task: title, 
        done: completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));
    }
  },
  created(){
    axios.get('/todos')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err));
  }

}
</script>

<style>
  *{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

    body{
      text-align: center;
      font-family: Arial, Helvetica, sans-serif;
      line-height: 1.4;
      background-color: gray;
    }

    .btn{
      display: inline-block;
      background: #555;
      color: #fff;
      padding: 7px 20px;
      cursor: pointer;
    }

    .btn:hover {
      background: #666;
    }
</style>
