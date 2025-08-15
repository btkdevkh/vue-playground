<script setup lang="ts">
import { onMounted, ref } from 'vue'

const API_URL = 'http://localhost:8000/todos'

const title = ref('')
const editTitle = ref('')
const editingId = ref<string | null>(null)
const todos = ref<{ id: string; title: string }[] | null>(null)

const getTodos = async () => {
  const res = await fetch(API_URL)
  const data = await res.json()
  todos.value = data
}

const addTodo = async () => {
  if (!title.value) return

  await fetch(API_URL, {
    method: 'POST',
    headers: {
      'content-type': 'application/json',
    },
    body: JSON.stringify({
      id: Date.now().toString(),
      title: title.value,
    }),
  })

  title.value = ''
  getTodos()
}

const showEditForm = (todo: { id: string; title: string }) => {
  editingId.value = todo.id
  editTitle.value = todo.title
}

const editTodo = async (id: string) => {
  await fetch(`${API_URL}/${id}`, {
    method: 'PUT',
    headers: {
      'content-type': 'application/json',
    },
    body: JSON.stringify({
      id: id.toString(),
      title: editTitle.value,
    }),
  })

  editingId.value = null
  getTodos()
}

const deleteTodo = async (id: string) => {
  await fetch(`${API_URL}/${id}`, {
    method: 'DELETE',
  })

  todos.value = todos.value && todos.value.filter((todo) => todo.id !== id)
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
      <button class="bg-blue-700 px-3 py-1 rounded cursor-pointer">Ajouter</button>
    </form>

    <div v-for="todo in todos" :key="todo.id" class="flex gap-1 justify-between">
      <form
        v-if="editingId === todo.id"
        @submit.prevent="editTodo(todo.id)"
        class="w-full flex gap-1"
      >
        <input
          type="text"
          placeholder="Titre"
          v-model="editTitle"
          class="w-full px-2 outline-0 border border-white rounded"
        />
        <button class="bg-orange-400 px-2 rounded">Modifier</button>
      </form>

      <p v-else class="underline">{{ todo.title }}</p>

      <div class="flex gap-1">
        <button
          v-if="editingId !== todo.id"
          @click="showEditForm(todo)"
          class="bg-orange-400 cursor-pointer px-3 rounded"
        >
          Update
        </button>
        <button @click="deleteTodo(todo.id)" class="bg-red-600 cursor-pointer px-3 rounded">
          Delete
        </button>
      </div>
    </div>
  </div>
</template>
