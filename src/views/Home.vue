<script setup>
import { ref } from 'vue'
import UploadDoc from '@/components/UploadDoc.vue'
import Reader from '@/components/Reader.vue'

// Texte global partagé
const text = ref('')
</script>

<template>
  <div class="min-h-screen bg-gray-100 p-6">

    <div class="max-w-2xl mx-auto bg-white p-6 rounded-xl shadow">

      <h1 class="text-2xl font-bold mb-4 text-center">
        📄 DocVoice AI
      </h1>

      <!-- Upload + OCR -->
      <UploadDoc @update:text="text = $event" />

      <!-- Lecture vocale -->
      <div v-if="text" class="mt-6 text-center">
        <Reader :text="text" />
      </div>

    </div>

  </div>
</template>
