<script lang="ts">
import { defineComponent, ref } from 'vue'
import { type PdfFile } from '@/models/file-pdf'

export const pdfs = ref<PdfFile[][]>([[], []])
export const draggedPdf = ref<{ sectionIndex: number; pdfIndex: number } | undefined>()

export const handleDragStart = (sectionIndex: number, pdfIndex: number) => {
  draggedPdf.value = { sectionIndex, pdfIndex }
}

export const handleDragOver = (sectionIndex: number, event: DragEvent) => {
  event.preventDefault()
}

// eslint-disable-next-line @typescript-eslint/no-unused-vars
export const handleDrop = (targetSectionIndex: number, event: DragEvent) => {
  if (draggedPdf.value !== undefined) {
    const { sectionIndex, pdfIndex } = draggedPdf.value
    if (sectionIndex !== targetSectionIndex) {
      const droppedPdf = pdfs.value[sectionIndex].splice(pdfIndex, 1)[0]
      if (!pdfs.value[targetSectionIndex]) {
        pdfs.value[targetSectionIndex] = [] // Initialize as an empty array if not defined
      }
      pdfs.value[targetSectionIndex].push(droppedPdf)
    }
    draggedPdf.value = undefined
  }
}

export const handleFileChange = (event: Event) => {
  const target = event.target as HTMLInputElement
  const file = target.files?.[0]
  if (file) {
    const pdfFile: PdfFile = {
      name: file.name,
      file: file
    }
    pdfs.value[0].push(pdfFile)
  }
}
export default defineComponent({
  name: 'HookPdfs'
})
</script>
<style>
.container {
  display: flex;
}

.hooks {
  background-color: lightblue;
  border-radius: 10px;
  padding: 10px;
  margin: 10px;
}

.header,
.content {
  background-color: lightblue;
  border-radius: 10px;
  padding: 10px;
  margin: 10px;
}
</style>
