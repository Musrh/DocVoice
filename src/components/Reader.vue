<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  text: {
    type: String,
    default: ''
  }
})

const speak = () => {
  if (!props.text) return

  const utterance = new SpeechSynthesisUtterance(props.text)
  utterance.lang = 'fr-FR'

  speechSynthesis.speak(utterance)
}
</script>

<template>
  <button @click="speak" :disabled="!text">
    🔊 Lire
  </button>
</template>
