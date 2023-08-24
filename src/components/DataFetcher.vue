<script setup lang="ts">
import { onMounted } from 'vue'

const props = defineProps({
  searchTerm: String,
  currentPage: Number
})

onMounted(() => {
  fetchData()
})

const emit = defineEmits(['submitted', 'characterData', 'totalPages', 'dataError'])

function fetchData() {
  fetch(
    `https://rickandmortyapi.com/api/character/?name=${props.searchTerm}&page=${props.currentPage}`
  )
    .then((response) => {
      if (response.ok) {
        return response.json()
      }
      return response.json().then((response) => {
        throw new Error(response.error)
      })
    })
    .then((data) => {
      emit('characterData', data.results)
      emit('totalPages', data.info.pages)
    })
    .catch((error) => {
      console.error('Error fetching data: ', error)
      emit('dataError', true)
    })
    .finally(() => {
      emit('submitted', false)
    })
}
</script>

<template lang="">
  <div class="loaderContainer">
    <div class="lds-ring">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>
  </div>
</template>

<style scoped>
.loaderContainer {
  display: flex;
  justify-content: center;
}

.lds-ring {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}

.lds-ring div {
  box-sizing: border-box;
  display: block;
  position: absolute;
  width: 64px;
  height: 64px;
  margin: 8px;
  border: 8px solid #fff;
  border-radius: 50%;
  animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  border-color: #fff transparent transparent transparent;
}
.lds-ring div:nth-child(1) {
  animation-delay: -0.45s;
}
.lds-ring div:nth-child(2) {
  animation-delay: -0.3s;
}
.lds-ring div:nth-child(3) {
  animation-delay: -0.15s;
}
@keyframes lds-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
