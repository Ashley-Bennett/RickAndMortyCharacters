<script setup lang="ts">
import SearchForm from '@/components/SearchForm.vue'
import DataFetcher from '@/components/DataFetcher.vue'
import CharacterCard from './components/CharacterCard/CharacterCard.vue'
import PaginationContainer from './components/Pagination/PaginationContainer.vue'
import { ref, watch } from 'vue'

const searchTerm = ref('')
const submitted = ref(false)
const characterData: any = ref(null)
const currentPage = ref(1)
const totalPages: any = ref(0)
watch(currentPage, () => {
  characterData.value = null
  submitted.value = true
})

function searched() {
  submitted.value = true
  characterData.value = null
  currentPage.value = 1
}
</script>

<template>
  <main>
    <SearchForm @searchTerm="(term) => (searchTerm = term)" @submitted="searched()" />
    <div v-if="submitted">
      <DataFetcher
        :searchTerm="searchTerm"
        :currentPage="currentPage"
        @submitted="(resetSubmitted) => (submitted = resetSubmitted)"
        @characterData="(newCharacterData) => (characterData = newCharacterData)"
        @totalPages="(newTotalPages) => (totalPages = newTotalPages)"
      />
    </div>
    <div v-if="characterData">
      <div class="characterCardWrapper">
        <CharacterCard
          v-for="(character, index) in characterData"
          :key="index"
          :characterData="character"
        />
      </div>
      <PaginationContainer
        :totalPages="totalPages"
        @goToPage="(goToPage) => (currentPage = goToPage)"
      />
    </div>
  </main>
</template>

<style scoped>
.characterCardWrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
</style>
