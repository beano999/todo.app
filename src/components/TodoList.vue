<script setup>
import { ref } from 'vue';
import TodoListItem from './TodoListItem.vue';

// Reactive array to hold todos
const todos = ref([]);

// Function to create a new todo
const createTodo = () => {
  todos.value.push({
    id: todos.value.length + 1,
    title: `New Todo #${todos.value.length + 1}`,
    completed: false,
  });
};

// Function to delete a todo
const deleteTodo = (id) => {
//console.log('deleting: ', id);
  todos.value = todos.value.filter(todo => todo.id !== id);
  //console.log('remaining todos: ' , todos.value);
};
</script>

<template>
  <main>
    <div id="mainContainer" class="mainContainer">
      <button class="createButton" id="createTodo" v-on:click="createTodo">Create a New ToDo</button>
      
      <TodoListItem 
        v-for="todo in todos" 
        :key="todo.id" 
        :todo="todo" 
        @delete-todo="deleteTodo" 
      />
    </div>
  </main>
</template>

<style scoped>
.mainContainer {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: center;
  border-radius: 10px;
  background-color: #454545;
}

.createButton {
  background-color: #2c9e30;
  border: none;
  color: white;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 1.5rem;
  margin-inline: 40px;
  margin-block: 20px;
  cursor: pointer;
  border-radius: 10px;
  font-family: monospace , sans-serif;
  transition: 0.3s;
}

.createButton:hover {
  
  background-color: #225c25;
}
</style>
