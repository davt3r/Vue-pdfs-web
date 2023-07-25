<template>
  <div class="container">
    <div class="hooks">
      <section class="header" @dragover="handleDragOver(0, $event)" @drop="handleDrop(0, $event)">
        <input type="file" @change="handleFileChange" accept=".pdf" />
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
        <input type="file" @change="handleFileChange" accept=".pdf , .txt, .png" />

        <div
          v-for="(item, index) in pdfs[1]"
          :key="index"
          :draggable="true"
          @dragstart="handleDragStart(1, index)"
        >
          {{ item.name }}
        </div>
      </section>
      <section class="content" @dragover="handleDragOver(2, $event)" @drop="handleDrop(2, $event)">
        <input type="file" @change="handleFileChange" accept=".png" />

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
  </div>
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
  components: {},
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

.sidebar {
  background-color: lightgreen;
  border-radius: 10px;
  padding: 10px;
  margin: 10px;
}
</style>
