<template>
  <section class="sidebar" @dragover="handleDragOver(3, $event)" @drop="handleDrop(3, $event)">
    <input type="file" @change="handleFileChange" accept=".pdf , .txt" />

    <div
      v-for="(item, index) in pdfs[3]"
      :key="index"
      :draggable="true"
      @dragstart="handleDragStart(3, index)"
    >
      {{ item.name }}
    </div>
  </section>
</template>

<script lang="ts">
import {
  pdfs,
  handleDragStart,
  handleDragOver,
  handleDrop,
  handleFileChange
} from '@/hooks/hooks-pdf.vue'

export default {
  setup() {
    return {
      pdfs,
      handleDragStart,
      handleDragOver,
      handleDrop,
      handleFileChange
    }
  }
}
</script>

<style>
.sidebar {
  background-color: lightgreen;
  border-radius: 10px;
  padding: 10px;
  margin: 10px;
}

.sidebar > div {
  margin-bottom: 10px;
}
</style>
