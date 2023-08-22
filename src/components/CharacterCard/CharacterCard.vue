<script setup lang="ts">
import CharacterCardInfoBox from '@/components/CharacterCard/CharacterCardInfoBox.vue'
import { ref } from 'vue'
const props = defineProps({
  characterData: Object
})

const characterDataArray: any = ref()

if (props.characterData) {
  characterDataArray.value = [
    { dataName: 'Species', data: `${props.characterData.species} - ${props.characterData.gender}` },
    { dataName: 'Status', data: props.characterData.status },
    { dataName: 'Location', data: props.characterData.location.name },
    { dataName: 'Origin', data: props.characterData.origin.name }
  ]
}
</script>
<template lang="">
  <div>
    <h3>{{ characterData.name }}</h3>
    <img v-bind:src="characterData.image" alt="" srcset="" />
    <CharacterCardInfoBox
      v-for="(dataSet, index) in characterDataArray"
      :key="index"
      :dataName="dataSet.dataName"
      :data="dataSet.data"
    />
  </div>
</template>
<style lang=""></style>
