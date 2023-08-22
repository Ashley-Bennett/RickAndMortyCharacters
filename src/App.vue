<script setup lang="ts">
import SearchForm from '@/components/SearchForm.vue'
import DataFetcher from '@/components/DataFetcher.vue'
import { ref } from 'vue'

const searchTerm = ref('morty')
const submitted = ref(false)
</script>

<template>
  <main>
    <SearchForm
      @searchTerm="(term) => (searchTerm = term)"
      @submitted="(hasSubmitted) => (submitted = hasSubmitted)"
    />
    <div v-if="submitted"><DataFetcher :searchTerm="searchTerm" /></div>
    {{ searchTerm }}
  </main>
</template>

<style scoped></style>
