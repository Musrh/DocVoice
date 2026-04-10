<script setup>
import { ref } from 'vue'
import Tesseract from 'tesseract.js'

const text = ref('')
const loading = ref(false)
const error = ref('')

const handleFile = async (e) => {
  const file = e.target.files[0]
  if (!file) return

  // Reset
  error.value = ''
  text.value = ''

  // Vérifier type fichier
  if (!file.type.startsWith('image/')) {
    error.value = 'Veuillez uploader une image (jpg, png...)'
    return
  }

  try {
    loading.value = true

    const { data: { text: result } } = await Tesseract.recognize(
      file,
      'eng'
    )

    text.value = result

  } catch (err) {
    error.value = 'Erreur lors de la lecture du document'
    console.error(err)
  } finally {
    loading.value = false
  }
}
</script>

<template>
  <div class="p-4 border rounded-lg">

    <!-- Upload -->
    <input type="file" accept="image/*" @change="handleFile" />

    <!-- Loading -->
    <p v-if="loading">⏳ Lecture du document...</p>

    <!-- Error -->
    <p v-if="error" class="text-red-500">{{ error }}</p>

    <!-- Résultat -->
    <textarea
      v-if="text"
      v-model="text"
      rows="10"
      class="w-full mt-4 border p-2 rounded"
    />

  </div>
</template>
