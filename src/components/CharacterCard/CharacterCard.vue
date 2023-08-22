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
  <div class="characterCard">
    <h3 class="name">{{ characterData.name }}</h3>
    <img :src="characterData.image" alt="" srcset="" />
    <CharacterCardInfoBox
      v-for="(dataSet, index) in characterDataArray"
      :key="index"
      :dataName="dataSet.dataName"
      :data="dataSet.data"
    />
  </div>
</template>
<style scoped>
.characterCard {
  display: flex;
  flex-direction: column;
  border: #bfde42 17px solid;
  background: #42b4ca;
  max-width: 300px;
  height: 550px;
  border-radius: 20px;
  padding: 5px 20px;
  margin: 20px;
}

.characterCard img {
  max-width: 314px;
  border: #bfde42 6px solid;
  border-radius: 5px;
}

.name {
  color: white;
}
</style>
