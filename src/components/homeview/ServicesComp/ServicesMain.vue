<script setup>
import TitleServices from './TitleServices.vue';
import CardService from './CardService.vue';

// Dados dos serviços
const services = [
  {
    id: 1,
    image: 'https://th.bing.com/th/id/R.1da2db9f3c0657ab512726165fc6e9c9?rik=6nGA1XuvwR889Q&pid=ImgRaw&r=0',
    title: 'Banho & Tosa',
    description: 'Cuidado completo com os melhores shampoos e técnicas de tosa por raça',
    features: [
      'Tosa na Máquina/Tesoura',
      'Corte de Unhas',
      'Limpeza de Ouvidos',
    ]
  },
  {
    id: 2,
    image: 'https://petderma.com.br/wp-content/uploads/2025/02/petderma-hidratacao-da-pele-em-pets.3-1024x683.jpg',
    title: 'Hidratação',
    description: 'Cronograma capilar para fios sedosos, brilhantes e pele saudável',
    features: [
      'Máscaras nutritivas',
      'Recuperação de pelagem',
      'Brilho Intenso',
    ]
  },
  {
    id: 3,
    image: 'https://res.cloudinary.com/goengineco/image/upload/f_auto,q_auto,c_limit,w_750,fl_lossy/v1/pet-club/strapi-images/cuidado_canino_consejos_y_beneficios_de_llevar_a_tu_perro_a_la_estetica_ac9f63eb76',
    title: 'Estética',
    description: 'Procedimentos especializados para manter a beleza e padrão da raça.',
    features: [
        'Tosas da Raça',
        'Tosa Baby',
        'Penteados Criativos',
    ]
  }
];
</script>

<template>
  <section class="services" aria-labelledby="services-title">
    <TitleServices id="services-title" />
    
    <div class="services__container">
      <div class="services__cards">
        <CardService 
          v-for="service in services" 
          :key="service.id"
          :image="service.image"
          :title="service.title"
          :description="service.description"
          :features="service.features"
        />
      </div>
    </div>
  </section>
</template>

<style scoped>
.services {
  width: 100%;
  margin-top: 2rem;
  padding: 2rem 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 3rem;
  background-color: var(--color-background-light);
  position: relative;
}

.services::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 100px;
  z-index: 1;
}

.services__container {
  width: 90%;
  margin: 0 auto;
  position: relative;
  z-index: 2;
}

.services__cards {
  width: 100%;
  display: flex;
  gap: 2.5rem;
  padding: 0 1rem;
}

@media (max-width: 768px) {
  .services {
    margin-top: 2rem;
    padding: 1.5rem 0.5rem;
    gap: 2rem;
  }
  
  .services__cards {
    flex-direction: column;
    gap: 2rem;
    padding: 0 0.5rem;
  }
}

@media (min-width: 769px) and (max-width: 1024px) {
  .services__cards {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1025px) {
  .services__cards {
    grid-template-columns: repeat(4, 1fr);
  }
}
</style>