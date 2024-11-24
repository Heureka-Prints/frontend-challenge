<script setup lang="ts">
import MenuRatios from './menu-items-components/MenuRatios.vue'
import MenuShapes from './menu-items-components/MenuShapes.vue'
import MenuTextPreview from './menu-items-components/MenuTextPreview.vue'
import MenuThemes from './menu-items-components/MenuThemes.vue'
</script>

<template>
  <div class="menu-items-container">
    <div class="menu-items-wrapper">
      <MenuRatios />
    </div>
    <div class="menu-items-wrapper">
      <MenuShapes />
    </div>
    <div class="menu-items-wrapper">
      <MenuTextPreview />
    </div>
    <div class="menu-items-wrapper">
      <MenuThemes />
    </div>
  </div>
</template>

<style scoped>
@import '../../../assets/stylesheets/components/menu/menu-items.css';
</style>
