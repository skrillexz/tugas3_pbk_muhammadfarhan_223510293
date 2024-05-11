<template>
  <div class="container">
    <h1>To Do List</h1>
    <input type="text" v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task...">
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <template v-if="editedIndex !== index">
          <span>{{ task }}</span>
          <button @click="removeTask(index)">Remove</button>
          <button @click="editTask(index)">Edit</button>
        </template>
        <template v-else>
          <input type="text" v-model="tasks[index]" @keyup.enter="updateTask(index)" placeholder="Edit task...">
          <button @click="updateTask(index)">Update</button>
          <button @click="cancelEdit">Cancel</button>
        </template>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const newTask = ref('');
const editedIndex = ref(null);
const tasks = ref([]);

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
};

const removeTask = (index) => {
  tasks.value.splice(index, 1);
};

const editTask = (index) => {
  editedIndex.value = index;
};

const updateTask = (index) => {
  editedIndex.value = null;
};

const cancelEdit = () => {
  editedIndex.value = null;
};
</script>

<style scoped>
.container {
  max-width: 400px;
  margin: 0 auto;
}

input[type="text"] {
  width: calc(100% - 100px);
  margin-bottom: 10px;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 5px;
}

button {
  padding: 5px 10px;
  margin-left: 5px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background-color: #007bff;
  color: #fff;
}

button:hover {
  background-color: #0056b3;
}
</style>
