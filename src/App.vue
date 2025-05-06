<script setup>
import { ref, computed } from 'vue';

const tasks = ref([]);
const newTask = ref('');
const fiter = ref('all');

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

const filteredTasks = computed(() => {
  if (fiter.value === 'completed') {
    return tasks.value.filter((task) => task.completed);
  } else if (fiter.value === 'incomplete') {
    return tasks.value.filter((task) => !task.completed);
  } else {
    return tasks.value;
  }
});

</script>

<template>
  <div>
    <input type="text" v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
    <button @click="addTask">Add Task</button>
    <select v-model="fiter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="incomplete">Incomplete</option>
    </select>

    <ul>
      <li v-for="task in filteredTasks" :key="task.id">
        <input type="checkbox" @change="toggleTaskCompletion(task)" v-model="task.completed" />
        {{ task.description }}
        <button @click="deleteTask(task)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
