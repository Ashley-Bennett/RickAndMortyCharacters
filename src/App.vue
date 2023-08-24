<script setup lang="ts">
import { ref, watch } from 'vue'
import SearchForm from '@/components/SearchForm.vue'
import DataFetcher from '@/components/DataFetcher.vue'
import CharacterCard from './components/CharacterCard/CharacterCard.vue'
import PaginationContainer from './components/Pagination/PaginationContainer.vue'
import annoyedRick from '../src/assets/annoyedRick.png'
import logo from '../src/assets/Rick_and_Morty_Logo.svg'

const searchTerm = ref('')
const submitted = ref(false)
const characterData: any = ref(null)
const currentPage = ref(1)
const totalPages: any = ref(0)
const dataError = ref(false)

watch(currentPage, () => {
  characterData.value = null
  submitted.value = true
})

function searched() {
  submitted.value = true
  characterData.value = null
  dataError.value = false
  currentPage.value = 1
}
</script>

<template>
  <main>
    <div class="logoContainer">
      <img class="logo" :src="logo" alt="" srcset="" />
      Character Database
    </div>
    <SearchForm @searchTerm="(term) => (searchTerm = term)" @submitted="searched()" />
    <div v-if="submitted">
      <DataFetcher
        :searchTerm="searchTerm"
        :currentPage="currentPage"
        @dataError="(setDataError) => (dataError = setDataError)"
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
        :currentPage="currentPage"
        @goToPage="(goToPage) => (currentPage = goToPage)"
      />
    </div>
    <div v-if="dataError" class="dataErrorContainer">
      <p>
        We have an error from the back-end, certainly not the front-end, or user based that's for
        sure. Maybe try again later or try a different character's name, maybe one that exists?
      </p>
      <img :src="annoyedRick" alt="" srcset="" />
    </div>
  </main>
</template>

<style scoped>
.logoContainer {
  display: flex;
  align-items: center;
  flex-direction: column;
}

.logo {
  max-width: 500px;
}

.characterCardWrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.dataErrorContainer {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.dataErrorContainer p {
  font-size: 40px;
  color: white;
}

.dataErrorContainer img {
  width: 500px;
  position: absolute;
  bottom: 0;
}
@media only screen and (max-width: 600px) {
  .logo {
    max-width: 300px;
  }

  .dataErrorContainer p {
    font-size: 20px;
    color: white;
  }
}
@media only screen and (max-width: 760px) {
  .characterCardWrapper {
    justify-content: center;
  }
}
</style>
