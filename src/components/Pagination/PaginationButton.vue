<script setup lang="ts">
import { ref } from 'vue'

const props = defineProps({
  pageNumber: Number,
  currentPage: Number
})

const emit = defineEmits(['pageSelected'])
const isCurrentPage = ref(false)

function handlePageClick(pageNumber: Number) {
  emit('pageSelected', pageNumber)
}

function handleCurrentPageClass() {
  if (props.currentPage === props.pageNumber) {
    isCurrentPage.value = true
  }
}

handleCurrentPageClass()
</script>

<template lang="">
  <button :class="{ selected: isCurrentPage }" v-on:click="handlePageClick(pageNumber)">
    {{ pageNumber }}
  </button>
</template>

<style scoped>
button {
  padding: 20px;
  color: #193840;
  border: none;
  border-radius: 5px;
  background: #bfde42;
  font-weight: 500;
  transition: all 0.2s ease-in-out;
}

.selected {
  background: #42b4ca;
  border: #bfde42 2px solid;
  color: white;
  font-weight: 700;
}
button:hover {
  scale: 1.1;
  cursor: pointer;
}
</style>
