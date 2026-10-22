<template>
  <div class="slidev-layout editorial cover">
    <header class="editorial-masthead">
      <span class="editorial-wordmark">filiphric.com</span>
      <span class="editorial-label">CypressConf 2026</span>
    </header>
    <main class="editorial-content" :class="{ 'with-cover-art': $slots.image }">
      <div class="cover-copy"><slot /></div>
      <div v-if="$slots.image" class="cover-art"><slot name="image" /></div>
    </main>
  </div>
</template>
