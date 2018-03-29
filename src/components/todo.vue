<template lang="pug">
  .todo
    todo-input(
      @addTodo="addNewTodo"
    )
    todo-list(
      :todos="todos"
      @checkTodo="checkTodo"
    )

</template>

<script>
import todoInput from './todoInput';
import todoList from './todoList';

import { eventBus } from '../main';

export default {
  components: {
    todoInput,
    todoList
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    addNewTodo(todo) {
      this.todos.push(todo);
    },
    checkTodo(todo) {
      this.todos = this.todos.map(item => (item.id === todo.id ? todo : item));
    }
  },
  mounted() {
    eventBus.$on('removeTodo', todoId => {
      this.todos = this.todos.filter(item => item.id !== todoId);
    });
  }
};
</script>
<style lang="scss" src="styles/todo.scss" scoped></style>