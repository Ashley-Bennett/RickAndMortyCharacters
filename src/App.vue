<script setup lang="ts">
import SearchForm from '@/components/SearchForm.vue'
import DataFetcher from '@/components/DataFetcher.vue'
import CharacterCard from './components/CharacterCard/CharacterCard.vue'
import { ref } from 'vue'

const searchTerm = ref('')
const submitted = ref(false)
const characterData = ref(null)
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
        @characterData="(newCharacterData) => (characterData = newCharacterData)"
      />
    </div>
    <div v-if="characterData">
      <CharacterCard
        v-for="(character, index) in characterData"
        :key="index"
        :characterData="character"
      />
      {{ characterData }}
    </div>
  </main>
</template>

<style scoped></style>
