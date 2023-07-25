<template>
  <div>
    <HeaderPdfs />
  </div>
  <div>
    <HookPdfs />
    <sideBar />
  </div>
  <sideBarVue />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import HeaderPdfs from './components/header-pdf.vue'
import HookPdfs from '@/hooks/hooks-pdf.vue'
import sideBarVue from './components/side-bar.vue'
import sideBar from './components/pdf-manager.vue'

export default defineComponent({
  components: {
    HookPdfs,
    HeaderPdfs,
    sideBarVue,
    sideBar
  }
})
</script>
<style>
#app {
  display: flex;
}
</style>
