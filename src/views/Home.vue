<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: [
      ]
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://my-json-server.typicode.com/thaivanluat/vuejs-todo-example/todos/${id}`).then(this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => console.log(err));
    },

    addTodo(newTodo) {
      // let id = this.todos.length + 1;
      // newTodo.id = id;
      // this.todos = [...this.todos, newTodo];

      const { title, completed } = newTodo;

      axios.post('https://my-json-server.typicode.com/thaivanluat/vuejs-todo-example/todos', {
        title,
        completed
      }).then(res => this.todos = [...this.todos, res.data])
      .catch(err => console.log(err))

    },
  },

  created() {
    axios.get('https://my-json-server.typicode.com/thaivanluat/vuejs-todo-example/todos').then(res => this.todos = res.data).catch(err => console.log(err));

    console.log(this.todos);
  }
}
</script>

<style>
* {
  box-sizing:border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
