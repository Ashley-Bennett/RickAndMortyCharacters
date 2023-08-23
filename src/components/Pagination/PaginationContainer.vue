<script setup lang="ts">
import PaginationButton from './PaginationButton.vue'
import { ref, watch } from 'vue'
const props = defineProps({
  totalPages: Number
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
      @pageSelected="(pageSelected) => (nextPageSelected = pageSelected)"
    />
  </ul>
</template>
<style></style>
