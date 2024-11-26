<script setup lang="ts">
import { reactive } from 'vue';
import MenuEditor from './components/MenuEditor.vue';
import PosterPreview from './components/PosterPreview.vue';

const posterSettings = reactive({
  text: 'Your Poster Text',  
  shape: 'heart',            
  aspectRatio: '2x3',
  bgColor: '#fff'
});

</script>

<template>
  <div class="product-editor">
    <!-- Poster Preview -->
    <div class="poster-preview__container poster-preview__animated">
      <PosterPreview  
      :shape="posterSettings.shape" 
      :aspectRatio="posterSettings.aspectRatio"
      :text="posterSettings.text"
      :bgColor="posterSettings.bgColor" 
      />
    </div>
    <!-- Menu Editor -->
    <div class="menu-editor__container menu-editor__animated">
      <MenuEditor  
      :settings="posterSettings" 
      />
    </div>
  </div>
</template>


<style scoped>
@import '@/assets/stylesheets/layout.css';

</style>