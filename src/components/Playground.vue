<script setup lang="ts">
import { ref } from 'vue'
import ReactiveStateExample from '../../examples/ReactiveStateExample.vue'

defineProps<{
  msg: string
}>()

const paragraph = ref('Ici, vous pouvez tester les fonctionnalités de Vue.js')
</script>

<template>
  <div class="playground">
    <h1 class="green">{{ msg }}</h1>
    <p>{{ paragraph }}</p>
  </div>
  <br />
  <hr />
  <br />

  <!-- Examples -->
  <div class="examples">
    <ReactiveStateExample />
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}
h3 {
  font-size: 1.2rem;
}
.playground h1,
.playground h3,
.playground p {
  text-align: center;
}

@media (min-width: 1024px) {
  .playground h1,
  .playground h3 {
    text-align: left;
  }
}
</style>
