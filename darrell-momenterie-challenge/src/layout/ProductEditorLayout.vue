<template>
  <main class="editor-grid">
    <section class="preview-grid-item">
      <slot name="preview" />
    </section>
    <aside class="menu-grid-item">
      <slot name="menu" />
    </aside>
  </main>
</template>

<style scoped>
@import '../assets/stylesheets/layout/main-layout.css';
</style>
