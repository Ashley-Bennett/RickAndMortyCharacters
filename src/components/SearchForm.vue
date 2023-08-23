<script setup lang="ts">
import { ref } from 'vue'
const emit = defineEmits(['searchTerm', 'submitted'])
const searchTerm = ref(null)
const hasError = ref(false)
const wobble = ref(false)

function handleSubmit() {
  wobble.value = false

  if (searchTerm.value) {
    console.log(searchTerm.value)
    hasError.value = false
    emit('searchTerm', searchTerm)
    emit('submitted', true)
    return ``
  }
  wobble.value = true
  hasError.value = true
}
</script>

<template lang="">
  <form @submit.prevent="handleSubmit">
    <input
      :class="{ error: hasError, wobble: wobble }"
      v-model="searchTerm"
      type="text"
      placeholder="Enter a character's name..."
    />
    <button type="submit">Search</button>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  width: 100%;
  justify-content: center;
  align-items: center;
}

input {
  margin-bottom: 20px;
  width: 100%;
  border-radius: 5px;
  height: 30px;
  padding: 16px 8px;
}

button {
  width: 100px;
  border-radius: 5px;
  background: #42b4ca;
  height: 30px;
  color: white;
}
.error {
  outline: red 1px solid;
  /* transition: all 0.2s ease-in-out; */
  animation-duration: 0.5s;
}

.wobble {
  animation-name: wobble;
}

@keyframes wobble {
  0% {
    transform: translateX(0%);
  }
  15% {
    transform: translateX(-10%);
  }
  30% {
    transform: translateX(10%);
  }
  45% {
    transform: translateX(-10%);
  }
  60% {
    transform: translateX(5%);
  }
  75% {
    transform: translateX(-5%);
  }
  100% {
    transform: translateX(0%);
  }
}
</style>
