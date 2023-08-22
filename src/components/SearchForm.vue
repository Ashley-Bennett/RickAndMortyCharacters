<script setup lang="ts">
import { ref } from 'vue'
const emit = defineEmits(['searchTerm', 'submitted'])
const searchTerm = ref('')

function handleSubmit() {
  console.log(searchTerm.value)
  emit('searchTerm', searchTerm)
  emit('submitted', true)
}
</script>

<template lang="">
  <form @submit.prevent="handleSubmit">
    <input v-model="searchTerm" type="text" />
    <button type="submit">Search</button>
  </form>
</template>

<style scoped></style>
