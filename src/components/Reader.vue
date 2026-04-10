<script setup>
const speak = (text) => {
  const utterance = new SpeechSynthesisUtterance(text)
  utterance.lang = 'fr-FR'
  speechSynthesis.speak(utterance)
}
</script>

<template>
  <button @click="speak(text)">
    🔊 Lire
  </button>
</template>
