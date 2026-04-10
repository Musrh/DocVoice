<script setup>
import { ref } from 'vue'
import Tesseract from 'tesseract.js'

const text = ref('')
const loading = ref(false)

const handleFile = async (e) => {
  const file = e.target.files[0]
  if (!file) return

  loading.value = true

  const { data: { text: result } } = await Tesseract.recognize(
    file,
    'eng'
  )

  text.value = result
  loading.value = false
}
</script>

<template>
  <div>
    <input type="file" @change="handleFile" />

    <p v-if="loading">Lecture du document...</p>

    <textarea v-if="text" v-model="text" rows="10" />
  </div>
</template>
