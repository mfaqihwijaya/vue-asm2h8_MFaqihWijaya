<template>
  <ol>
    <li v-for="todo in todos" :key="todo.id">
      <input type="checkbox" @change="changeStatus(todo.id)" />
      <span :class="{ completed: todo.completed }"
        ><strong class="textTodo">{{ todo.text }}</strong></span
      >
      <button @click="deleteThis(todo.id)" id="delete">Delete</button>
      <br />
      <span>Today:</span>
      <span>{{ todo.createdWhen }}</span>
      <br />
      <span>Deadline Date:</span>
      <span>{{ todo.deadline }}</span>
    </li>
  </ol>
</template>

<script>
export default {
  name: 'TodoItems',
  props: ['todos'],
  methods: {
    deleteThis(todoId) {
      this.$emit('deleteTodo', todoId);
    },
    changeStatus(todoId) {
      this.$emit('changeStatusTodo', todoId);
    },
  },
};
</script>

<style>
#delete {
  color: black;
  background: #f8b7cd;
}
</style>
