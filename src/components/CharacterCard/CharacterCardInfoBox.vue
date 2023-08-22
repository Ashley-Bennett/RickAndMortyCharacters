<script setup lang="ts">
const props = defineProps({
  dataName: String,
  data: String
})
</script>
<template lang="">
  <div>{{ dataName }}: {{ data }}</div>
</template>
<style lang=""></style>
