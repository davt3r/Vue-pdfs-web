<template>
  <div>
    <section class="sidebar">
      <div>
        <input type="file" @change="handleFileChangeText" accept=".txt" />
        <label>Documentos TXT</label>
      </div>
      <div>
        <input type="file" @change="handleFileChangeImage" accept="image/*" />
        <label>Imágenes</label>
      </div>
      <div>
        <input type="file" @change="handleFileChangeAll" accept=".txt,image/*" />
        <label>Todos los archivos</label>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import type { PdfFile } from '@/models/file-pdf'
import { ref } from 'vue'

const pdfs = ref<PdfFile[][]>([[], [], []])

const handleFileChangeText = (event: Event) => {
  const target = event.target as HTMLInputElement
  const file = target.files?.[0]

  if (file) {
    const pdfFile: any = {
      name: file.name,
      file: file
    }
    pdfs.value[0].push(pdfFile)
  }
}

const handleFileChangeImage = (event: Event) => {
  const target = event.target as HTMLInputElement
  const file = target.files?.[0]
  if (file) {
    if (file.type.startsWith('image/')) {
      const pdfFile: any = {
        name: file.name,
        file: file
      }
      pdfs.value[1].push(pdfFile)
    } else {
      console.warn('El archivo seleccionado no es una imagen.')
    }
  }
}

const handleFileChangeAll = (event: Event) => {
  const target = event.target as HTMLInputElement
  const file = target.files?.[0]
  if (file) {
    const pdfFile: any = {
      name: file.name,
      file: file
    }
    pdfs.value[2].push(pdfFile)
  }
}
</script>

<style>
.sidebar {
  background-color: lightgreen;
  border-radius: 10px;
  padding: 10px;
  margin: 10px;
  display: flex;
  flex-direction: column;
}

.sidebar > div {
  margin-bottom: 10px;
}
</style>
