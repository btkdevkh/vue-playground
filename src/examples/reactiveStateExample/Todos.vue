<script setup lang="ts">
import { defineProps } from "vue"
import TodoItem from "./Todo.vue"

defineProps<{
  todos: { id: string; title: string }[] | null
}>()

const emit = defineEmits(["getTodos"])
</script>
<template>
  <div v-for="todo in todos" :key="todo.id" class="flex gap-1 justify-between">
    <TodoItem :todo="todo" @getTodos="() => emit('getTodos')" />
  </div>
</template>
