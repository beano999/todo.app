<script setup>

// Props
const props= defineProps({
  todo: {
    type: Object,
    required: true,
  },
});

// Emit event for deleting todo
const emit = defineEmits(['delete-todo']);

const handleDelete = () => {
  emit('delete-todo', props.todo.id);
};
</script>

<template>
  <div class="todo-item">
    <h2 id="todoTitle">{{ todo.title }}</h2>
    <button class="delete-button" v-on:click="handleDelete">Delete</button>
  </div>
</template>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  background-color: #555555;
  border-radius: 10px;
  margin: 10px;
  padding: 10px;
  color: white;
}

.delete-button {
  background-color: red;
  border: none;
  color: white;
  cursor: pointer;
  border-radius: 5px;
  padding: 5px 10px;
  transition: 0.3s;
}

.delete-button:hover {
  background-color: darkred;
}
</style>
