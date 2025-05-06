<script setup>
import { ref } from 'vue';

const tasks = ref([
  { id: 1, description: 'Task 1', completed: false },
  { id: 2, description: 'Task 2', completed: true },
  { id: 3, description: 'Task 3', completed: false },
]);

const newTask = ref('');

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push({
      id: tasks.value.length + 1,
      description: newTask.value,
      completed: false,
    });
    newTask.value = '';
  }
};

</script>

<template>
  <div>
    <input type="text" v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
    <button @click="addTask">Add Task</button>
    
    <ul>
      <li v-for="task in tasks" :key="task.id">
        {{  task.description }} - {{ task.completed ? 'Completed' : 'Not Completed' }}
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
