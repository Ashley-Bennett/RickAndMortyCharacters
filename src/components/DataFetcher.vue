<script setup lang="ts">
import { onMounted, reactive } from 'vue'

const props = defineProps({
  searchTerm: String,
  currentPage: Number
})

onMounted(() => {
  console.log('here')
  console.log(props)
  fetchData()
})

const emit = defineEmits(['submitted', 'characterData', 'totalPages', 'dataError'])

function fetchData() {
  console.log(props.searchTerm)

  fetch(
    `https://rickandmortyapi.com/api/character/?name=${props.searchTerm}&page=${props.currentPage}`
  )
    .then((response) => {
      if (response.ok) {
        console.log(response)
        return response.json()
      }
      throw response
    })
    .then((data) => {
      console.log(data)
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
<template lang="">loading</template>
<style lang=""></style>
