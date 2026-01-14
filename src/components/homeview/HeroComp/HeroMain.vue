<template>
  <section class="hero-main">
    <div class="container-main">
      <div class="one">
        <InfoComp />
      </div>

      <div class="photo-wrapper">
        <PhotoComp />
      </div>
    </div>
  </section>
</template>

<script setup>
import InfoComp from './InfoComp.vue'
import PhotoComp from './PhotoComp.vue'
</script>

<style scoped>
.hero-main {
  width: 100%;
  min-height: 80vh;
  font-family: var(--font-display);
  margin-top: 2rem;
}

.container-main {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  width: 90%;
  min-height: 80vh;
  margin: 0 auto;
}

.one {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

/* Wrapper dá altura pro carousel */
.photo-wrapper {
  min-height: 450px;
}

/* MOBILE */
@media (max-width: 1024px) {
  .container-main {
    display: flex;
    flex-direction: column;
    gap: 3rem;
    min-height: auto;
  }

  .hero-main {
    min-height: auto;
  }

  .photo-wrapper {
    min-height: 350px;
  }
}
</style>
