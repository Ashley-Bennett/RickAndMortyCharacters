<script setup lang="ts">
import PaginationButton from './PaginationButton.vue'
import { ref, watch } from 'vue'

const props = defineProps({
  totalPages: Number,
  currentPage: Number
})

const emit = defineEmits(['goToPage'])
const nextPageSelected = ref(0)

watch(nextPageSelected, (goToPage) => {
  emit('goToPage', goToPage)
})
</script>

<template lang="">
  <ul>
    <PaginationButton
      v-for="(pageNumber, index) in totalPages"
      :key="index"
      :pageNumber="pageNumber"
      :currentPage="currentPage"
      @pageSelected="(pageSelected) => (nextPageSelected = pageSelected)"
    />
  </ul>
</template>

<style scoped>
ul {
  display: flex;
  justify-content: space-between;
}
</style>
