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
};

const deleteTask = (task) => {
  tasks.value = tasks.value.filter((t) => t.id !== task.id);
};

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
  <div class="min-h-screen bg-rose-50 text-gray-800 flex items-start justify-center p-6">
    <div class="bg-white w-full max-w-6xl h-130 rounded-xl shadow-2xl flex flex-col md:flex-row overflow-hidden">

      <!-- Kiri: Form Input -->
      <div class="md:w-1/2 p-8 bg-rose-100 space-y-6 flex flex-col justify-between">
        <div class="space-y-4">
          <h2 class="text-2xl font-bold text-rose-600">✨ Tasya Mulyani</h2>
          <input v-model="newTask" @keyup.enter="addTask" type="text" placeholder="Tugas baru..."
            class="w-full px-4 py-2 rounded-lg border border-rose-300 focus:outline-none focus:ring-2 focus:ring-rose-400" />
          <button @click="addTask"
            class="w-full bg-rose-500 hover:bg-rose-600 text-white font-semibold py-2 rounded-lg transition">
            Tambahkan
          </button>
        </div>

        <div class="pt-4">
          <label class="block mb-1 text-rose-700 font-semibold">Filter:</label>
          <select v-model="fiter"
            class="w-full bg-white border border-rose-300 rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-rose-400">
            <option value="all">Semua</option>
            <option value="completed">Selesai</option>
            <option value="incomplete">Belum selesai</option>
          </select>
        </div>
      </div>

      <!-- Kanan: List Tugas -->
      <div class="md:w-1/2 p-8 bg-white overflow-y-auto max-h-[80vh]">
        <h2 class="text-2xl font-bold text-rose-600 mb-4">📋 Daftar Tugas</h2>
        <ul class="space-y-3">
          <li v-for="task in filteredTasks" :key="task.id"
            class="flex justify-between items-center bg-rose-50 border border-rose-200 px-4 py-3 rounded-lg shadow-sm">
            <div class="flex items-center gap-3">
              <input type="checkbox" v-model="task.completed" @change="toggleTaskCompletion(task)"
                class="accent-rose-500 w-4 h-4" />
              <span :class="{ 'line-through text-gray-400': task.completed }">
                {{ task.description }}
              </span>
            </div>
            <button @click="deleteTask(task)" class="text-rose-400 hover:text-rose-600 font-bold text-xl">
              ✕
            </button>
          </li>
        </ul>
      </div>

    </div>
  </div>
</template>
