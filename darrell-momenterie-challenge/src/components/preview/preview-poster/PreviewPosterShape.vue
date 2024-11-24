<script lang="ts" setup>
import { inject } from 'vue'

const shapeSrc = inject<string>('shape')
const hueRotate = inject<number>('hue-rotate')
const saturate = inject<number>('saturate')
</script>

<template>
  <img
    :src="shapeSrc"
    alt="shape"
    width="70%"
    :style="{ filter: `hue-rotate(${hueRotate}deg) saturate(${saturate})` }"
  />
</template>

<style scoped>
@import '../../../assets/stylesheets/components/preview/preview-shape.css';
</style>
