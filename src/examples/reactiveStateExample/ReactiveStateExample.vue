<script setup lang="ts">
import { onMounted, ref } from "vue"
import TodosList from "./Todos.vue"

const API_URL = "http://localhost:8000/todos"

const title = ref("")
const todos = ref<{ id: string; title: string }[]>([])

const getTodos = async () => {
  const res = await fetch(API_URL)
  const data = await res.json()
  todos.value = data
}

const addTodo = async () => {
  if (!title.value) return

  await fetch(API_URL, {
    method: "POST",
    headers: {
      "content-type": "application/json",
    },
    body: JSON.stringify({
      id: Date.now().toString(),
      title: title.value,
    }),
  })

  title.value = ""
  getTodos()
}

onMounted(() => {
  getTodos()
})
</script>

<template>
  <div class="flex flex-col gap-2">
    <h2>CRUD "reactive state"</h2>
    <form @submit.prevent="addTodo" class="flex gap-1">
      <input
        type="text"
        placeholder="Titre"
        v-model="title"
        class="w-full px-2 outline-0 border border-gray-500 rounded"
      />
      <button class="bg-blue-700 px-3 py-1 rounded cursor-pointer">Valider</button>
    </form>

    <TodosList :todos="todos" @getTodos="getTodos" />
  </div>
</template>
