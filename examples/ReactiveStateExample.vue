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
  <!-- Reactive state example -->
  <div>
    <div>
      <p>"CRUD example with "reactive state"</p>

      <form @submit.prevent="addTodo">
        <input type="text" placeholder="Titre" v-model="title" />
        <button>Ajouter</button>
      </form>

      <div v-for="todo in todos" :key="todo.id" class="todo">
        <form v-if="editingId === todo.id" @submit.prevent="editTodo(todo.id)">
          <input type="text" placeholder="Titre" v-model="editTitle" />
          <button>Modifier</button>
        </form>
        <span v-else>{{ todo.title }}</span>
        <button v-if="editingId !== todo.id" @click="showEditForm(todo)">Modifier</button>
        <button v-if="editingId !== todo.id" @click="deleteTodo(todo.id)">x</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.todo {
  display: flex;
  gap: 0.2rem;
}
</style>
