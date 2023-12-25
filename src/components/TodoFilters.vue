<template>
  <div class="actions">
    <p>{{ filterTodo.length }} todos</p>
    <div class="filter">
      <button
        @click="changeFilterStatus('all')"
        :class="{ selected: filterStatus === 'all' }"
      >
        All
      </button>
      <button
        @click="changeFilterStatus('active')"
        :class="{ selected: filterStatus === 'active' }"
      >
        Active
      </button>
      <button
        @click="changeFilterStatus('completed')"
        :class="{ selected: filterStatus === 'completed' }"
      >
        Completed
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    filterTodo: {
      type: Array,
      required: true,
    },
    filterStatus: {
      type: String,
      required: true,
    },
  },
  emits: ["changeStatus"],
  methods: {
    changeFilterStatus(status) {
      this.$emit("changeStatus", status);
    },
  },
};
</script>

<style scoped>
.actions {
  padding: 1rem 0rem;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.actions .filter button {
  margin-right: 0.5rem;
  padding: 0.5rem 1rem;
  border: none;
  outline: none;
  border-radius: 0.5rem;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
}
.actions .filter button.selected {
  background: #172554;
  color: #f3f4f6;
}
</style>
