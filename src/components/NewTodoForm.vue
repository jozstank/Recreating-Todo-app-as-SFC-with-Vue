<template>
  <form action="#" @submit.prevent="$emit('addTodo', this.todoTitle)">
    <input
      type="text"
      placeholder="What needs to be done?"
      v-model="todoTitle"
    />
  </form>
</template>

<script>
export default {
  data() {
    return {
      todoTitle: "",
    };
  },
  emits: ["addTodo"],
};
</script>

<style scoped>
form input {
  width: 100%;
  height: 50px;
  padding: 1rem;
  font-size: 1.5rem;
  font-weight: 600;
  border: none;
  outline: none;
  border-radius: 0.5rem;
}
</style>
