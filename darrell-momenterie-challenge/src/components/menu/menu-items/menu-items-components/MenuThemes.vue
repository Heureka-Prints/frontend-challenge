<script lang="ts" setup>
import { inject } from 'vue'

const hueRotate = inject<number>('hue-rotate')
const saturate = inject<number>('saturate')
const handleImageReset = inject<() => void>('handle-image-reset')
</script>

<template>
  <h3>Themes</h3>
  <fieldset>
    <label for="white_theme"
      >White
      <input type="radio" id="default-checkbox" name="theme" checked />
    </label>
    <label for="dark_gold_theme"
      >Dark Gold
      <input type="radio" id="dark-gold-checkbox" name="theme" />
    </label>
    <label for="dark_theme"
      >Dark
      <input type="radio" id="dark-checkbox" name="theme" />
    </label>
  </fieldset>
  <fieldset>
    <label>
      Image Hue
      <input v-model="hueRotate" type="range" max="360" min="0" />
    </label>
    <label>
      Image Saturation
      <input v-model="saturate" type="range" max="3" min="0" step="0.1" />
    </label>
    <button @click="handleImageReset">Reset</button>
  </fieldset>
</template>

<style scoped>
@import '../../../../assets/stylesheets/components/inputs/fieldset.css';
@import '../../../../assets/stylesheets//components/inputs/range.css';
@import '../../../../assets//stylesheets//components/menu/menu-items-components.css';
</style>
