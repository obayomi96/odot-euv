<template>
  <div id="app">
    <!-- <Header /> -->
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from '../components/Todos';
// import Header from '../components/layout/Header';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    // Header,
    AddTodo,
  }, data() {
    return {
      todos: [
        // {
        //   id: 1,
        //   title: 'Todo one',
        //   completed: false,
        // },
        // {
        //   id: 2,
        //   title: 'Todo two',
        //   completed: false,
        // },
        // {
        //   id: 3,
        //   title: 'Todo three',
        //   completed: false,
        // }
      ],
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => this.todos = this.todos.filter(todo => todo.id !== id, res.data))
      .catch(err => `errr${err}`)
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios.post("https://jsonplaceholder.typicode.com/todos", {
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(err => `errr${err}`)
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todos = res.data)
    .catch(err => `errr${err}`);
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
