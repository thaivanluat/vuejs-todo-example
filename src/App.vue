<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';

export default {
  name: 'App',
  components: {
    Header,
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "To do 1",
          completed: false
        },
        {
          id: 2,
          title: "To do 2",
          completed: false
        },
        {
          id: 3,
          title: "To do 3",
          completed: false
        }
      ]
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },

    addTodo(newTodo) {
      let id = this.todos.length + 1;
      newTodo.id = id;
      this.todos = [...this.todos, newTodo];
    }
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
