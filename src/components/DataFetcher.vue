<script setup lang="ts">
import { onMounted, reactive } from 'vue'

const props = defineProps({
  searchTerm: String
})

onMounted(() => {
  console.log('here')
  console.log(props)
  fetchData()
})

const emit = defineEmits(['submitted', 'characterData'])

function fetchData() {
  fetch(`https://rickandmortyapi.com/api/character/?name=${props.searchTerm}&page=1`)
    .then((response) => {
      if (response.ok) {
        console.log(response)
        return response.json()
      }
      throw response
    })
    .then((data) => {
      console.log(data)
      emit('characterData', data)
    })
    .catch((error) => {
      console.error('Error fetching data: ', error)
    })
    .finally(() => {
      // loading logic
      emit('submitted', false)
    })
}
</script>
<template lang="">Loading</template>
<style lang=""></style>
