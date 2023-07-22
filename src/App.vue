<template>
  <div>
    <HeaderPdfs />
    <HookPdfs />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import HeaderPdfs from './components/header-pdf.vue'
import HookPdfs from './hooks/hooks-pdf.vue'

export default defineComponent({
  components: {
    HookPdfs,
    HeaderPdfs
  }
})
</script>
