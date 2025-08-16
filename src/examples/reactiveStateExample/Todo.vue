<script setup lang="ts">
import { defineProps, defineEmits, ref } from "vue"

const API_URL = "http://localhost:8000/todos"

const props = defineProps<{
  todo: { id: string; title: string }
}>()

const emit = defineEmits(["getTodos"])

const editTitle = ref(props.todo.title)
const isEditing = ref(false)

const showEditForm = () => {
  isEditing.value = true
}

const editTodo = async (id: string, title: string) => {
  await fetch(`${API_URL}/${id}`, {
    method: "PUT",
    headers: {
      "content-type": "application/json",
    },
    body: JSON.stringify({
      id: id.toString(),
      title,
    }),
  })

  isEditing.value = false
  emit("getTodos")
}

const deleteTodo = async (id: string) => {
  await fetch(`${API_URL}/${id}`, {
    method: "DELETE",
  })
  emit("getTodos")
}
</script>
<template>
  <form v-if="isEditing" @submit.prevent="editTodo(todo.id, editTitle)" class="w-full flex gap-1">
    <input
      type="text"
      placeholder="Titre"
      v-model="editTitle"
      class="w-full px-2 outline-0 border border-white rounded"
    />
    <button class="bg-orange-400 px-2 rounded">Valider</button>
  </form>
  <p v-else class="underline">{{ todo.title }}</p>

  <div class="flex gap-1">
    <button
      v-if="!isEditing"
      @click="showEditForm"
      class="bg-orange-400 cursor-pointer px-3 rounded"
    >
      Update
    </button>
    <button @click="deleteTodo(todo.id)" class="bg-red-600 cursor-pointer px-3 rounded">
      Delete
    </button>
  </div>
</template>
