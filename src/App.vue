<script setup>
import { ref } from 'vue';

const tasks = ref([
  { id: 1, description: 'Task 1', completed: false },
  { id: 2, description: 'Task 2', completed: true },
  { id: 3, description: 'Task 3', completed: false },
]);

</script>

<template>
  <div>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        {{  task.description }} - {{ task.completed ? 'Completed' : 'Not Completed' }}
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
