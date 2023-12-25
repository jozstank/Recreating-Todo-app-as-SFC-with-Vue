<template>
  <ul class="todo-list">
    <template v-if="todos.length > 0">
      <li class="todo-item" v-for="todo in filterTodo" :key="todo.id">
        <input type="checkbox" v-model="todo.completed" />
        <span class="todo-title" :class="{ completed: todo.completed }">{{
          todo.title
        }}</span>
        <span class="todo-remove" @click="emitDeleteTodo(todo.id)">
          &times;
        </span>
      </li>
    </template>
    <li v-else class="todo-item">No todos found</li>
  </ul>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true,
    },
    filterTodo: {
      type: Array,
      required: true,
    },
  },
  emits: ["deleteTodo", "setFilterStatus"],
  methods: {
    emitDeleteTodo(x) {
      this.$emit("deleteTodo", x);
    },
  },
};
</script>

<style scoped>
.todo-list {
  list-style: none;
  margin-top: 1rem;
}
.todo-item {
  font-size: 1.5rem;
  font-weight: 600;
  padding: 1rem 0rem;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}
.todo-item input {
  margin-right: 1rem;
  width: 1.5rem;
  height: 1.5rem;
  border-radius: 50%;
  border: 1px solid #333;
  outline: none;
  cursor: pointer;
  appearance: none;
  -webkit-appearance: none;
  vertical-align: middle;
}
.todo-item input:checked {
  background: #172554;
}
.todo-title.completed {
  text-decoration: line-through;
}
.todo-remove {
  float: right;
  cursor: pointer;
}
</style>
