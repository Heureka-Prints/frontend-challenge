<script lang="ts" setup>
import { inject } from 'vue'

const handleShapeChange = inject<() => void>('handle-shape-change')
</script>

<template>
  <h3>Shape</h3>
  <div class="button-container">
    <button @click="handleShapeChange" value="src/assets/images/shape-circle.svg">Circle</button>
    <button @click="handleShapeChange" value="src/assets/images/shape-heart.svg">Heart</button>
    <button @click="handleShapeChange" value="src/assets/images/shape-square.svg">Square</button>
    <button @click="handleShapeChange" value="src/assets/images/shape-star.svg">Star</button>
    <button @click="handleShapeChange" value="src/assets/images/shape-triangle.svg">
      Triangle
    </button>
  </div>
</template>

<style scoped>
@import '../../../../assets/stylesheets/components/inputs/button-generic.css';
@import '../../../../assets//stylesheets//components/menu/menu-items-components.css';
</style>
