<script setup lang="ts">
import { ref } from 'vue'
// import OptionApi from '@/examples/OptionApiExample.vue'
// import CompositionApiExample from '@/examples/CompositionApiExample.vue'
// import ReactiveStateExample from '@/examples/ReactiveStateExample.vue'

defineProps<{
  msg: string
}>()

const paragraph = ref('Ici, vous pouvez tester les fonctionnalités de Vue.js')
</script>

<template>
  <div class="text-center">
    <h1 class="green text-2xl">{{ msg }}</h1>
    <p>{{ paragraph }}</p>
  </div>
  <br />
  <hr />
  <br />

  <!-- Examples -->
  <div>
    <!-- <OptionApi /> -->
    <!-- <CompositionApiExample /> -->
    <!-- <ReactiveStateExample /> -->
  </div>
</template>
