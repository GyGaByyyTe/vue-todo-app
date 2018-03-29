<template lang="pug">
  .todo-list(v-if="todos.length")
    .content
      ul.list
        li.item(v-for="todoItem in filteredTodos")
          todo-item(
            :todo="todoItem"
            @checkTodo="checkTodo"
          )
    .footer
      .footer-content
        .counter
          | Кол-во заданий: {{filteredTodos.length}}
        .filter
          button(
            v-for="item in filters"
            type="button"
            @click="applyFilter(item)"
            :class="{active: currentFilter === item}"
          ) {{item}}

</template>
<script>
import todoItem from './todoItem';

export default {
  components: {
    todoItem
  },
  props: {
    todos: Array
  },
  data: () => ({
    filters: ['all', 'active', 'completed'],
    currentFilter: 'all'
  }),
  computed: {
    filteredTodos() {
      switch (this.currentFilter) {
        case 'all':
          return this.todos;
        case 'active':
          return this.todos.filter(item => !item.checked);
        case 'completed':
          return this.todos.filter(item => item.checked);
      }
    }
  },
  methods: {
    applyFilter(filter) {
      this.currentFilter = filter;
    },
    checkTodo(todo) {
      this.$emit('checkTodo', todo);
    }
  }
};
</script>
<style src="styles/todoList.scss" lang="scss" scoped></style>