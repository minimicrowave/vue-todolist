<template>
  <div>
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";

import axios from "axios";

export default {
  name: "Home",
  components: { Todos, AddTodo },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    async deleteTodo(id) {
      await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    async addTodo(newTodo) {
      const { title, completed } = newTodo;

      const { data: newTodoWithID } = await axios.post(
        "https://jsonplaceholder.typicode.com/todos",
        {
          title,
          completed
        }
      );
      this.todos = [...this.todos, newTodoWithID];
    }
  },
  async created() {
    const { data: todos } = await axios.get(
      "https://jsonplaceholder.typicode.com/todos?_limit=5"
    );
    this.todos = todos;
  }
};
</script>

<style>
* {
  box-sizing: 0;
  padding: 0;
}

body {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  color: white;
  background: #555;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
