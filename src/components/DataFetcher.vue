<script setup lang="ts">
import { onMounted, reactive } from 'vue'
const characterData = reactive({})
const props = defineProps({
  searchTerm: String
})
onMounted(() => {
  console.log('here')
  console.log(props)

  fetchData()
})
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
    })
    .catch((error) => {
      console.error('Error fetching data: ', error)
    })
    .finally(() => {
      // loading logic
    })
}
</script>
<template lang="">
  <button @click="fetchData">get ricks</button>
</template>
<style lang=""></style>
