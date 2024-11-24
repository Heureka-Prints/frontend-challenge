<script setup lang="ts">
import { inject } from 'vue'
import PreviewPosterShape from './PreviewPosterShape.vue'

const aspectRatio = inject<string>('ratio')
const previewText = inject<string>('preview-text')
</script>

<template>
  <div class="poster-container" :style="{ aspectRatio }">
    <div class="poster-content-container">
      <PreviewPosterShape />
      <div class="preview-text-container">
        <h2>{{ previewText }}</h2>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import '../../../assets/stylesheets/components/preview/preview-poster.css';
</style>
