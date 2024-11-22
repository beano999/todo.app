<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
  todo: { type: Object, required: true },
});
const emit = defineEmits(['delete-todo', 'update-todo']);

const isEditing = ref(false);
const editedTitle = ref(props.todo.title);

// Ensure editedTitle updates if todo title changes externally
watch(() => props.todo.title, (newTitle) => {
  editedTitle.value = newTitle;
});

// Function for deleting (emits event to todolist.vue)
const handleDelete = () => {
  emit('delete-todo', props.todo.id);
};
// Function for saving the edit (emits event to todolist.vue)
const saveEdit = () => {
  if (editedTitle.value.trim() !== '') {
    emit('update-todo', props.todo.id, editedTitle.value);  // Emit updated title
    isEditing.value = false;
  }
};
</script>

<template>
  <div class="todo-item">
    <!-- Editing view -->
    <div v-if="isEditing" class="edit-mode">
      <input v-model="editedTitle" @keyup.enter="saveEdit" class="edit-input" />
      <button class="save-button" @click="saveEdit">Save</button>
      <button class="cancel-button" @click="isEditing = false">Cancel</button>
    </div>

    <!-- Normal view -->
    <div v-else class="normal-mode">
      <div class="todo-content">
        <input type="checkbox" v-model="todo.completed" class="check" />
        <h2 :class="{ completed: todo.completed }">{{ todo.title }}</h2>
      </div>
      <div class="button-group">
        <button class="edit-button" @click="isEditing = true">Edit</button>
        <button class="delete-button" @click="handleDelete">Delete</button>
      </div>
    </div>
  </div>
</template>


<!-- Scoped styles / this is an absolute mess but it works ... my computer bluescreened this morning but i got it working and have been frantically coding for some time now-->
<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: linear-gradient(145deg, #444444, #555555);
  border-radius: 12px;
  padding: 15px;
  margin: 10px 0;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.todo-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
}

.todo-content {
  display: flex;
  align-items: center;
}

.todo-content h2 {
  font-size: 1.2rem;
  color: white;
  margin-left: 10px;
}

.completed {
  text-decoration: line-through;
  color: #bbb;
}

.check {
  width: 20px;
  height: 20px;
  margin-right: 10px;
  accent-color: #2c9e30;
  cursor: pointer;
}

.button-group {
  display: flex;
  gap: 10px;
}

button {
  background-color: #2c9e30;
  border: none;
  color: white;
  padding: 8px 12px;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #225c25;
}

.delete-button {
  background-color: #ff4d4d;
}

.delete-button:hover {
  background-color: #cc0000;
}

.edit-button {
  background-color: #2c9e30;
}

.edit-input {
  padding: 8px;
  font-size: 1rem;
  border-radius: 8px;
  border: 1px solid #ccc;
}
</style>
