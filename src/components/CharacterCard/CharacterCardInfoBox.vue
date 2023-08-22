<script setup lang="ts">
const props = defineProps({
  dataName: String,
  data: String
})
</script>
<template lang="">
  <div class="infoBoxWrapper">
    <p class="bold">{{ dataName }}:</p>
    <p>
      {{ data }}
    </p>
  </div>
</template>
<style>
.infoBoxWrapper {
  display: flex;
  justify-content: space-between;
  background: #bfde42;
  margin: 10px 0;
  color: #193840;
  border-radius: 5px;
  padding: 5px;
}
.bold {
  font-weight: bold;
}
</style>
