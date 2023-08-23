<script setup lang="ts">
const props = defineProps({
  pageNumber: Number
})
const emit = defineEmits(['pageSelected'])

function handlePageClick(pageNumber: Number) {
  emit('pageSelected', pageNumber)
}
</script>
<template lang="">
  <button v-on:click="handlePageClick(pageNumber)">{{ pageNumber }}</button>
</template>
<style></style>
