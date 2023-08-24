<script setup lang="ts">
import { ref } from 'vue'
const emit = defineEmits(['searchTerm', 'submitted'])
const searchTerm = ref(null)
const hasError = ref(false)
const wobble = ref(false)

function handleSubmit() {
  wobble.value = false

  if (searchTerm.value) {
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
  <form @submit.prevent="handleSubmit" :class="{ error: hasError, wobble: wobble }">
    <input v-model="searchTerm" type="text" placeholder="Enter a character's name..." />
    <button type="submit">Search</button>
  </form>
  <i v-if="hasError">You need a name ya dingus</i>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: row;
  border: 1px solid #42b4ca;
  padding: 1px;
  border-radius: 5px;
  height: 50px;
}

input {
  border-radius: 3px 0 0 3px;
  font-size: 20px;
  flex-grow: 2;
  border: none;
  padding-left: 20px;
}

input:focus {
  outline: none;
}

form:focus-within {
  outline: 1px solid #bfde42;
}

button {
  border: 1px solid #42b4ca;
  background: #42b4ca;
  color: white;
  width: 200px;
}
.error {
  outline: red 2px solid;
  animation-duration: 0.5s;
}

.wobble {
  animation-name: wobble;
}

@media only screen and (max-width: 600px) {
  input {
    width: 100%;
  }

  button {
    width: 100px;
  }
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
