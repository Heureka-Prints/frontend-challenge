<script setup lang="ts">
import MenuItems from './menu-items/MenuItems.vue'
defineProps<{
  showAddToCart: boolean
}>()
</script>

<template>
  <div class="menu-container">
    <h2>Options</h2>
    <form @submit.prevent>
      <MenuItems />
      <div class="add-to-cart-container">
        <button :disabled="!showAddToCart">Add to Cart</button>
      </div>
    </form>
  </div>
</template>

<style scoped>
@import '../../assets/stylesheets/layout/menu-layout.css';
@import '../../assets/stylesheets/components/menu/menu.css';
@import '../../assets//stylesheets/components/inputs/button-addtocart.css';
</style>
