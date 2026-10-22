<template>
  <div class="slidev-layout editorial illustration">
    <main class="editorial-content">
      <div class="illustration-copy"><slot /></div>
      <div class="illustration-image"><slot name="image" /></div>
    </main>
    <footer class="editorial-footer">
      <span class="editorial-wordmark">filiphric.com</span>
      <span>CypressConf 2026</span>
    </footer>
  </div>
</template>
