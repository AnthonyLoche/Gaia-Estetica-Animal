<script setup>
import CardServiceSection from './CardServiceSection.vue';

import Dog from 'vue-material-design-icons/Dog.vue';
import ContentCut from 'vue-material-design-icons/ContentCut.vue';
import Shimmer from 'vue-material-design-icons/Shimmer.vue';
import Car from 'vue-material-design-icons/Car.vue';

const services = [
  {
    title: 'Banho',
    description:
      'Limpeza completa com shampoos específicos para cada tipo de pelo.',
    linkText: 'SAIBA MAIS',
    variant: 'pink',
    icon: Dog
  },
  {
    title: 'Tosa',
    description:
      'Tosa higiênica na máquina ou tesoura, respeitando o padrão da raça.',
    linkText: 'SAIBA MAIS',
    variant: 'green',
    icon: ContentCut
  },
  {
    title: 'Estética Animal',
    description:
      'Hidratação profunda, reconstrução de pelos e cuidados especiais.',
    linkText: 'SAIBA MAIS',
    variant: 'pink',
    icon: Shimmer
  },
  {
    title: 'Serviço de Táxi',
    description:
      'Buscamos e levamos seu pet com segurança e conforto.',
    linkText: 'CONSULTAR TAXA',
    variant: 'dark-green',
    icon: Car
  }
];
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
        <CardServiceSection
          v-for="service in services"
          :key="service.title"
          :title="service.title"
          :description="service.description"
          :link-text="service.linkText"
          :variant="service.variant"
        >
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
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 640px) {
  .section-title {
    font-size: 32px;
  }

  .services-grid {
    grid-template-columns: 1fr;
  }
}
</style>
