<script setup lang="ts">
import { reactive } from 'vue'
const characterData = reactive({})

function fetchData(charcterName: string) {
  fetch('https://rickandmortyapi.com/api/character/?name=rick&page=1')
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
