<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Header,
    Todos,
    AddTodo
  },
  data(){
    return{
      todos: []
    }
  },
  methods:{
    deleteTodo(id){

      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}
      `)
        .then(this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err => console.log(err));
    },
    addTodo(newTodo){

      const {title, completed } = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
        .then(res => this.todos = [...this.todos,newTodo, res.data])
        .catch(err=>console.log(err))
    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=3')
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
.btn{
  display: inline-block;
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 8px 20px;
  text-align: center;
  text-decoration: none;
}
body{
  font-family: Arial, sans-serif;
  line-height: 1.4rem;
}
</style>
