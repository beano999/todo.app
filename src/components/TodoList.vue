<script setup>
import TodoListItem from './TodoListItem.vue';
</script>
<template>
    <main>
        <div class = "mainContainer">
            <h1>List:</h1>
            <button class = "button" id ="createTodo">Create a ToDo</button>
            <TodoListItem />
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
    background-color: green;
}

.button {
    background-color: #4CAF50;
    border: none;
    color: white;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border-radius: 10px;
}

.button:hover {
    background-color: #45a049;
}
</style>