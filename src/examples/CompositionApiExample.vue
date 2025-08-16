<!-- Long version -->
<!-- <script lang="ts">
import { ref } from 'vue'

export default {
  setup() {
    // Data
    let text = ref("Hi, I'm a Vue component that use a composition api.")
    const info = 'https://vuejs.org/'

    // Methods
    const showDescription = () => {
      text.value = `${text.value} lorem...`
    }

    return {
      text,
      info,
      showDescription,
    }
  },
}
</script> -->

<!-- Short version with setup attribute in script tag -->
<script setup lang="ts">
import { ref } from 'vue'

// Data
const text = ref("Hi, I'm a Vue component that use a composition api.")
const info = 'https://vuejs.org/'

// Methods
const showDescription = () => {
  text.value = `${text.value} lorem...`
}
</script>

<template>
  <h1>{{ text }}</h1>

  <!-- <a v-bind:href="info" target="_blank">More info</a> -->
  <a :href="info" target="_blank">More info</a>

  <!-- <button v-on:click="() => console.log(123)">Click</button> -->
  <!-- <button @click="() => console.log(123)">Click</button> -->
  <button @click="showDescription">Click</button>
</template>

<style></style>
