<script lang="ts" setup>
import { inject } from 'vue'

const previewText = inject<string>('preview-text')
</script>

<template>
  <h3
    :style="{
      color: previewText?.length === 115 ? 'var(--error-red-color)' : 'var(--main-text-color)',
    }"
  >
    Text {{ `(${previewText?.length} /115)` }}
  </h3>
  <textarea v-model="previewText" placeholder="Enter text here" maxlength="115" type="text" />
</template>

<style scoped>
@import '../../../../assets/stylesheets/components/inputs/text-area.css';
@import '../../../../assets//stylesheets//components/menu/menu-items-components.css';
</style>
