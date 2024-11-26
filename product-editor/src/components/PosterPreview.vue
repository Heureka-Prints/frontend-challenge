<script setup lang="ts">

import { ref, computed, onMounted, onUnmounted } from 'vue';
const props = defineProps({
    aspectRatio: {
        type: String,
        default: '2x3'
    },
    shape: {
        type: String,
        default: 'heart',
        required: true,
    },
    text: {
        type: String,
    },
    bgColor: {
        type: String,
        default: '#ffff',
  },
})


const pathToSvg = computed (() => {
    const availableShapes: string[] = ['circle', 'heart', 'square', 'star', 'triangle'];
    const validShape: string = availableShapes.includes(props.shape) ? props.shape : 'heart'; //Fallback
    return `../src/assets/resources/shape-${validShape}.svg`;

})
const viewportWidth = ref<number>(window.innerWidth);

// Update the viewport width on resize
const updateViewportWidth = (): void => {
  viewportWidth.value = window.innerWidth;
};

// Listen to window resize
onMounted(() : void=> {
  window.addEventListener('resize', updateViewportWidth);
});
onUnmounted(() :void => {
  window.removeEventListener('resize', updateViewportWidth);
});

const posterStyle = computed(() => {
  const width = Math.min(viewportWidth.value * 0.4, 400); // 80% of viewport or max 400px for responsivenesss

  const [ratioWidth, ratioHeight] = props.aspectRatio ? props.aspectRatio.split('x').map(Number): [2, 3]; //Fallback
  const height = Math.round(width * (ratioHeight / ratioWidth));

  return {
    width: `${width}px`,
    height: `${height}px`,
    backgroundColor: props.bgColor,
  };
});

</script>

<template>
    <!-- The product is a simple poster with a shape and some text on it. -->
    <div class="poster-view poster-view__content" :style="posterStyle">
        <!-- Shape of poster  -->
         <div class="poster-view__shape"> <img :src="pathToSvg" alt="Poster Shape" /></div>
       
        <!-- Text on the poster -->
        <div class="poster-view__text"> {{ text }} </div>
    </div>
</template>

<style scoped>
  @import '@/assets/stylesheets/component-preview.css';
</style>