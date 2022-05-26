<script setup lang="ts">
import { ref } from 'vue'

import selectorTool from '@/components/selector-tool.vue'
const selection = ref()
</script>

<template>
  <div>
      <selector-tool @select="selection = $event"/>
      {{selection}}
  </div>
</template>

<style>
#app{
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
body{
  margin: 0px;
}
</style>