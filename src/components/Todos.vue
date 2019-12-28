<template>
  <div>
    <div v-bind:key="todo.id" v-for="(todo, index) in todos">
      <TodoItem v-bind:todo="todo" v-bind:index="index" v-on:del-todo="$emit('del-todo', todo.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
  name: "Todos",
  components: { TodoItem },
  props: ["todos"]
};
</script>

<style scoped>
</style>