<script lang="ts">
export default {
  // Data
  data() {
    return {
      text: "Hi, I'm a Vue component that use an option api.",
      info: 'https://vuejs.org/',
    }
  },

  // Methods
  methods: {
    showDescription() {
      this.text = `${this.text} lorem...`
    },
  },
}
</script>

<template>
  <h1>{{ text }}</h1>

  <!-- <a v-bind:href="info" target="_blank">More info</a> -->
  <a :href="info" target="_blank">More info</a>

  <!-- <button v-on:click="() => console.log(123)">Click</button> -->
  <button @click="() => console.log(123)">Click</button>
</template>

<style></style>
