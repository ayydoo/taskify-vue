<script setup>

import { ref } from "vue"

// simpan variable tasks sebagai array kosong
const tasks = ref([])
const taskInput = ref("")

// function untuk menambahkan task baru
const addTask = () => {

  // jika taskInput kosong, maka tidak menambahkan task baru
  if (taskInput.value.trim() === "") return alert("Task tidak boleh kosong")

  // membuat object task baru
  const newTask = {
    id: tasks.value.length + 1,
    title: taskInput.value,
    isDone: false
  }

  // push task baru ke array tasks
  tasks.value.push(newTask)

  // kosongkan inputan task
  taskInput.value = ""
}

// function untuk menghapus task
const removeTask = (id) => {

  // minta konfirmasi sebelum menghapus task
  const isConfirmed = confirm("Apakah anda yakin ingin menghapus task ini?")
  
  if (!isConfirmed) return

  // cek apakah task dengan id yang diberikan ada di array tasks
  const taskIndex = tasks.value.findIndex(task => task.id === id)
  
  if (taskIndex !== -1) {
    // hapus task dari array tasks
    tasks.value.splice(taskIndex, 1)
  }
}

</script>

<template>
  <!-- container -->
  <main class="max-w-2xl mx-auto p-8 rounded-lg bg-white shadow-md mt-10">
    <h1 class="text-2xl text-center text-gray-600 font-bold mb-4">Taskify Vue</h1>
    
    <form @submit.prevent="addTask" class="mb-4" action="">

      <!-- task field input -->
      <input v-model="taskInput" type="text" placeholder="Enter your task"
        class="border border-gray-300 rounded-md p-2 w-full mb-4" />
      <!-- action: add -->
      <button type="submit" class="bg-blue-500 text-white rounded-md p-2 w-full">Add Task</button>
    </form>

    <!-- task list -->
    <ul class="mt-4">

      <template v-for="task in tasks" :key="task.id">
        <li class="flex items-center justify-between border-b border-gray-300 py-2">
          <div>
            <input v-model="task.isDone" type="checkbox" class="mr-2" />
            <span :class="task.isDone ? 'line-through' : ''">{{ task.title }}</span>
          </div>
          <button @click="removeTask(task.id)" class="bg-red-500 text-white rounded-md p-1">
            Delete
          </button>
        </li>
      </template>
    
    </ul>
  </main>
</template>