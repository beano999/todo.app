<script setup>
import AppHeader from './components/AppHeader.vue';
import TodoList from './components/TodoList.vue';
</script>

<template>
  <header>
    <AppHeader />
  </header>

  <main>
    <TodoList />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

main{
  padding-top: 5em;
}

</style>
