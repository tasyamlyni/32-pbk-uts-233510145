<script setup>
import { ref } from 'vue';

const tasks = ref([]);

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

const toggleTaskCompletion = (task) => {
  task.completed == !task.completed;
}

const deleteTask = (task) => {
  tasks.value = tasks.value.filter((t) => t.id !== task.id);
}

</script>

<template>
  <div>
    <input type="text" v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
    <button @click="addTask">Add Task</button>

    <ul>
      <li v-for="task in tasks" :key="task.id">
        <input type="checkbox" @change="toggleTaskCompletion(task)" v-model="task.completed" />
        {{ task.description }}
        <button @click="deleteTask(task)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
