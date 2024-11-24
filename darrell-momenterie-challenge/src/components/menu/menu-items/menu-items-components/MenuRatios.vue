<script lang="ts" setup>
import { inject } from 'vue'

const handleRatioChange = inject<() => void>('handle-ratio-change')
</script>

<template>
  <h3>Ratios</h3>
  <div class="button-container">
    <button @click="handleRatioChange" type="button" value="2/3">2/3</button>
    <button @click="handleRatioChange" type="button" value="3/4">3/4</button>
    <button @click="handleRatioChange" type="button" value="5/7">5/7</button>
  </div>
</template>

<style scoped>
@import '../../../../assets/stylesheets/components/inputs/button-generic.css';
@import '../../../../assets//stylesheets//components/menu/menu-items-components.css';
</style>
