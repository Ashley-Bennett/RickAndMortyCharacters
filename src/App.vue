<script setup lang="ts">
import SearchForm from '@/components/SearchForm.vue'
import DataFetcher from '@/components/DataFetcher.vue'
import { ref } from 'vue'

const searchTerm = ref('')
const submitted = ref(false)
</script>

<template>
  <main>
    <SearchForm
      @searchTerm="(term) => (searchTerm = term)"
      @submitted="(hasSubmitted) => (submitted = hasSubmitted)"
    />
    <div v-if="submitted">
      <DataFetcher
        :searchTerm="searchTerm"
        @submitted="(resetSubmitted) => (submitted = resetSubmitted)"
      />
    </div>
    {{ searchTerm }}
  </main>
</template>

<style scoped></style>
