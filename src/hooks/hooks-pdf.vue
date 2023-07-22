<template>
  <div>
    <section class="header" @dragover="handleDragOver(0, $event)" @drop="handleDrop(0, $event)">
      <input type="file" @change="handleFileChange" accept=".pdf , .txt" />
      <div
        v-for="(item, index) in pdfs[0]"
        :key="index"
        :draggable="true"
        @dragstart="handleDragStart(0, index)"
      >
        {{ item.name }}
      </div>
    </section>

    <section class="content" @dragover="handleDragOver(1, $event)" @drop="handleDrop(1, $event)">
      <div
        v-for="(item, index) in pdfs[1]"
        :key="index"
        :draggable="true"
        @dragstart="handleDragStart(1, index)"
      >
        {{ item.name }}
      </div>
    </section>

    <section class="sidebar" @dragover="handleDragOver(2, $event)" @drop="handleDrop(2, $event)">
      <input type="file" @change="handleFileChange" accept=".pdf , .txt" />

      <div
        v-for="(item, index) in pdfs[2]"
        :key="index"
        :draggable="true"
        @dragstart="handleDragStart(2, index)"
      >
        {{ item.name }}
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { PdfFile } from '@/models/file-pdf'

const pdfs = ref<PdfFile[][]>([[], [], []])
const draggedPdf = ref<{ sectionIndex: number; pdfIndex: number } | undefined>()

const handleDragStart = (sectionIndex: number, pdfIndex: number) => {
  draggedPdf.value = { sectionIndex, pdfIndex }
}

const handleDragOver = (sectionIndex: number, event: DragEvent) => {
  event.preventDefault()
}

// eslint-disable-next-line @typescript-eslint/no-unused-vars
const handleDrop = (targetSectionIndex: number, event: DragEvent) => {
  if (draggedPdf.value !== undefined) {
    const { sectionIndex, pdfIndex } = draggedPdf.value
    if (sectionIndex !== targetSectionIndex) {
      const droppedPdf = pdfs.value[sectionIndex].splice(pdfIndex, 1)[0]
      pdfs.value[targetSectionIndex].push(droppedPdf)
    }
    draggedPdf.value = undefined
  }
}

const handleFileChange = (event: Event) => {
  const target = event.target as HTMLInputElement
  const file = target.files?.[0]
  if (file) {
    const pdfFile: PDFFile = {
      name: file.name,
      file: file
    }
    pdfs.value[0].push(pdfFile)
  }
}
</script>

<style>
.header,
.content,
.sidebar {
  background-color: lightblue;
  border-radius: 10px;
  padding: 10px;
  margin: 10px;
}
</style>
