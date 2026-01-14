<template>
  <header class="page-header">
    <div class="texture-bg"></div>
    <div class="header-content">
      <span class="badge">Institucional</span>
      <h1 class="main-title">Quem Somos</h1>
      <p class="header-description">
        Mais que estética, um gesto de amor e cuidado humanizado com quem você mais ama.
      </p>
    </div>
  </header>
</template>

<script setup>
// Nenhuma lógica necessária por enquanto
</script>

<style scoped>
.page-header {
  position: relative;
  padding: 6rem 0;
  overflow: hidden;
}

.texture-bg {
  position: absolute;
  inset: 0;
  opacity: 0.05;
}

.header-content {
  position: relative;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  text-align: center;
}

.badge {
  display: inline-block;
  padding: 0.375rem 1rem;
  margin-bottom: 1.5rem;
  font-size: 0.875rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  background-color: rgba(232, 168, 177, 0.2);
  color: var(--primary);
  border-radius: 9999px;
}

.dark .badge {
  color: var(--accent);
}

.main-title {
  font-family: var(--font-display), serif;
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  line-height: 1.2;
  color: var(--primary);
}

.dark .main-title {
  color: var(--white);
}

@media (min-width: 768px) {
  .main-title {
    font-size: 4.5rem;
  }
}

.header-description {
  font-size: 1.25rem;
  max-width: 36rem;
  margin: 0 auto;
  color: var(--text-light);
  line-height: 1.75;
}

.dark .header-description {
  color: var(--text-dark);
}

/* Responsividade adicional */
@media (max-width: 640px) {
  .page-header {
    padding: 4rem 0;
  }
  
  .main-title {
    font-size: 2.5rem;
  }
  
  .header-description {
    font-size: 1.125rem;
    padding: 0 1rem;
  }
}
</style>