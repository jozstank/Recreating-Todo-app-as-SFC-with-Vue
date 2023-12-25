<template>
  <NewTodoForm @addTodo="addNewToDo" ref="myElement"></NewTodoForm>
  <TodoItem
    @deleteTodo="deleteTodo"
    :filterTodo="filterTodo"
    :todos="todos"
  ></TodoItem>
  <TodoFilters
    @changeStatus="changeFilterStatus"
    :filterTodo="filterTodo"
    :filterStatus="filterStatus"
  ></TodoFilters>
</template>

<script>
import NewTodoForm from "./components/NewTodoForm.vue";
import TodoItem from "./components/TodoItem.vue";
import TodoFilters from "./components/TodoFilters.vue";
export default {
  data() {
    return {
      todos: [],
      todoTitle: "",
      filterStatus: "all",
      totalTodos: 0,
    };
  },

  computed: {
    filterTodo() {
      if (this.filterStatus === "all") {
        return this.todos;
      }
      if (this.filterStatus === "active")
        return this.todos.filter((x) => x.completed === false);
      if (this.filterStatus === "completed") {
        return this.todos.filter((x) => x.completed === true);
      }
    },
  },
  watch: {
    "filterTodo.length": {
      handler() {
        this.totalTodos = this.filterTodo.length;
      },
      immediate: true,
    },
  },
  methods: {
    addNewToDo(data) {
      this.todoTitle = data;
      if (this.todoTitle.length > 0) {
        const newTodo = {
          id: this.todos.length + 1,
          title: this.todoTitle,
          completed: false,
        };
        this.todos.push(newTodo);
        this.$refs.myElement.$data.todoTitle = "";
      }
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    changeFilterStatus(x) {
      this.filterStatus = x;
    },
  },
  components: {
    NewTodoForm,
    TodoItem,
    TodoFilters,
  },
};
</script>
