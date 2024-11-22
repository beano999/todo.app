<script setup>
import { ref, onMounted, watch } from 'vue';
import TodoListItem from './TodoListItem.vue';

const todos = ref(JSON.parse(localStorage.getItem('todos')) || []);

//this function creates a new todo by pushing a new object to the todos array and sets completed to false by default

const createTodo = () => {
  todos.value.push({
    id: Date.now(),  // Unique ID
    title: 'New Todo',
    completed: false,
  });
};

// Update the title of a specific todo by finding the todo with the matching ID (which is date.now so that it is always unique)
const updateTodo = (id, newTitle) => {
  const todo = todos.value.find(todo => todo.id === id);
  if (todo) {
    todo.title = newTitle;
  }
};

// Save to localStorage whenever todos change (this is so they don't disappear when the page is refreshed)
watch(todos, () => {
  localStorage.setItem('todos', JSON.stringify(todos.value));
}, { deep: true });


// Delete a todo by filtering out the todo with the matching ID (date.now)
const deleteTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id);
};
</script>

<template>
  <div class="mainContainer">
    <h2>COMP 206 - Assignment 2 - Ben Wartman</h2>
    <button class = "createButton" @click="createTodo">Create a New ToDo</button>
    <TodoListItem 
      v-for="todo in todos" 
      :key="todo.id" 
      :todo="todo" 
      @delete-todo="deleteTodo" 
      @update-todo="updateTodo" 
    />
  </div>
</template>

<style scoped>
.mainContainer {
  display: flex;
  flex-direction: column;
  align-items: center; 
  padding: 20px;
  background-color: #454545;
  border-radius: 10px;
  margin: 20px;
}

.createButton {
  background-color: #2c9e30;
  border: none;
  color: white;
  padding: 10px 20px;
  margin: 20px 0;  
  font-size: 1.5rem;
  cursor: pointer;
  border-radius: 10px;
  transition: 0.3s;
}

.createButton:hover {
  background-color: #225c25;
}
</style>