<script setup lang="ts">
import ProductEditorLayout from '../layout/ProductEditorLayout.vue'
import MenuComponent from '@/components/menu/MenuComponent.vue'
import PreviewComponent from '@/components/preview/PreviewComponent.vue'
import { ref, watch, type Ref, provide } from 'vue'

const aspectRatio: Ref<string> = ref('2/3')
const shapeSrc: Ref<string> = ref('src/assets/images/shape-circle.svg')
const text: Ref<string> = ref('How soon is now?')
const hueRotate: Ref<number> = ref(0)
const saturate: Ref<number> = ref(1)
const showAddToCart: Ref<boolean> = ref(false)

const handleRatioChange = (e: Event) => {
  const input = e.target as HTMLInputElement
  aspectRatio.value = input.value
}
const handleShapeChange = (e: Event) => {
  const input = e.target as HTMLInputElement
  shapeSrc.value = input.value
}

const handleImageReset = () => {
  hueRotate.value = 0
  saturate.value = 1
}

watch(text, (newText) => {
  if (newText) {
    showAddToCart.value = true
  }
})

provide('ratio', aspectRatio)
provide('shape', shapeSrc)
provide('preview-text', text)
provide('hue-rotate', hueRotate)
provide('saturate', saturate)
provide('handle-ratio-change', handleRatioChange)
provide('handle-shape-change', handleShapeChange)
provide('handle-image-reset', handleImageReset)
</script>

<template>
  <ProductEditorLayout>
    <template #preview>
      <PreviewComponent />
    </template>
    <template #menu>
      <MenuComponent :showAddToCart />
    </template>
  </ProductEditorLayout>
</template>
