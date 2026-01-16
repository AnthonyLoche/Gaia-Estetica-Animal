<script setup>
import CardServiceSection from './CardServiceSection.vue';
import { services } from '@/data/services';
</script>

<template>
  <section class="services-section">
    <div class="container">
      <h2 class="section-title">Nossos Serviços</h2>

      <p class="section-description">
        Oferecemos cuidado profissional e carinhoso para seu pet. Cada serviço é
        realizado com produtos de alta qualidade e muita dedicação.
      </p>

      <div class="services-grid">
        <CardServiceSection v-for="service in services" :key="service.title" :title="service.title"
          :description="service.description" :link-text="service.linkText" :variant="service.variant"
          :whatsapp-message="service.whatsappMessage">
          <template #icon>
            <component :is="service.icon" />
          </template>
        </CardServiceSection>

      </div>
    </div>
  </section>
</template>

<style scoped>
.services-section {
  width: 100%;
  padding: 80px 0;
}

.container {
  width: 90%;
  margin: 0 auto;
}

.section-title {
  font-size: 4rem;
  font-weight: 700;
  color: var(--color-primary);
  text-align: center;
  margin-bottom: 16px;
}

.section-description {
  font-size: 1rem;
  color: #5a6a66;
  text-align: center;
  max-width: 700px;
  margin: 0 auto 50px;
  line-height: 1.6;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
}

@media (max-width: 1024px) {
    .services-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 640px) {
  .section-title {
    font-size: 32px;
  }


}
</style>
