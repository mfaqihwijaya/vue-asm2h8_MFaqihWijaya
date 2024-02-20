<template>
  <h1>TODO APP</h1>
  <div class="container">
    <TodoBoard
      :todos="todos"
      @addTodo="addTodo"
      @deleteTodo="deleteTodo"
      @changeStatusTodo="changeStatusTodo"
    />
  </div>
</template>

<script setup>
import TodoBoard from './components/TodoBoard.vue';
import { ref } from 'vue';
const todos = ref([]);
function addTodo(newTodo) {
  todos.value.push(newTodo);
}
function deleteTodo(todoId) {
  todos.value = todos.value.filter((todo) => todo.id !== todoId);
}
function changeStatusTodo(todoId) {
  const todoIndex = todos.value.findIndex((todo) => todo.id === todoId);
  todos.value[todoIndex].completed = !todos.value[todoIndex].completed;
}
</script>

<style scoped>
.container {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 30px;
}

h1 {
  margin: 32px;
  text-align: center;
  color: #f8b7cd;
}
</style>
