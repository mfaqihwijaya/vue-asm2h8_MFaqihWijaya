<template>
  <div>
    <form @submit.prevent="addNewTodo">
      <input type="text" v-model="newTodoText" placeholder="Add New.." />
      <input type="date" id="date" v-model="selectedDate" />
      <button type="submit" id="button">Add Todo</button>
    </form>
    <TodoItems
      :todos="todos"
      @deleteTodo="deleteTodo"
      @changeStatusTodo="changeStatusTodo"
    />
  </div>
</template>

<script>
import TodoItems from './TodoItems.vue';

export default {
  name: 'TodoBoard',
  components: {
    TodoItems,
  },
  props: ['todos'],
  data() {
    return {
      selectedDate: null,
      newTodoText: '',
    };
  },
  methods: {
    addNewTodo() {
      if (this.newTodoText.trim() !== '') {
        const createdDate = new Date(Date.now());

        const newTodo = {
          id: Date.now(),
          createdWhen: createdDate.toISOString().split('T')[0],
          text: this.newTodoText,
          completed: false,
          deadline: this.selectedDate,
        };
        this.$emit('addTodo', newTodo);
        this.newTodoText = '';
      }
    },
    deleteTodo(todoId) {
      this.$emit('deleteTodo', todoId);
    },
    changeStatusTodo(todoId) {
      this.$emit('changeStatusTodo', todoId);
    },
  },
};
</script>

<style>
#button {
  color: black;
  background: #f8b7cd;
}
</style>
