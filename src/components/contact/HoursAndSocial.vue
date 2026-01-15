<template>
  <div class="info-section">
    <!-- Hours -->
    <section class="hours-section">
      <h3 class="hours-title">
        <Clock :size="24" />
        Horário de Funcionamento
      </h3>
      
      <ul class="hours-list">
        <li 
          v-for="hour in hours" 
          :key="hour.day" 
          class="hours-item"
          :class="{ closed: hour.closed }"
        >
          <span>{{ hour.day }}:</span>
          <span class="hours-time">{{ hour.time }}</span>
        </li>
      </ul>
    </section>

    <!-- Social Links -->
    <div class="social-links">
      <a 
        v-for="social in socialLinks" 
        :key="social.name"
        :href="social.link" 
        :target="social.external ? '_blank' : '_self'"
        class="social-link"
      >
        <component :is="social.icon" :size="32" class="social-icon" />
        <span class="social-text">{{ social.name }}</span>
      </a>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Clock from 'vue-material-design-icons/Clock.vue'
import Instagram from 'vue-material-design-icons/Instagram.vue'
import Phone from 'vue-material-design-icons/Phone.vue'
import Facebook from 'vue-material-design-icons/Facebook.vue'

const hours = ref([
  { day: 'Terça a Sexta', time: '08:00 - 12:00 e 13:30 - 18:00', closed: false },
  { day: 'Sábado', time: '08:00 – 13:00', closed: false },
  { day: 'Domingos e Feriados', time: 'Fechado', closed: true }
])

const socialLinks = ref([
  { 
    name: 'Instagram', 
    icon: Instagram, 
    link: 'https://www.instagram.com/gaiaesteticaanimal/',
    external: true 
  },
  { 
    name: 'Facebook', 
    icon: Facebook, 
    link: 'https://www.facebook.com/GaiaEsteticaAnimal',
    external: true 
  },
  { 
    name: 'Ligar', 
    icon: Phone, 
    link: 'tel:+554796180343',
    external: false 
  }
])
</script>

<style scoped>
.info-section {
  display: flex;
  flex-direction: column;
  gap: 40px;
}

.hours-section {
  background: #194031;
  color: white;
  padding: 32px;
  border-radius: 24px;
  box-shadow: 0 20px 40px rgba(25, 64, 49, 0.1);

}

.hours-title {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  gap: 12px;
}

.hours-list {
  list-style: none;
  padding: 0;
}

.hours-item {
  display: flex;
  justify-content: space-between;
  padding: 12px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.hours-item:last-child {
  border-bottom: none;
}

.hours-time {
  font-weight: 600;
}

.hours-item.closed {
  color: rgba(255, 255, 255, 0.6);
}

.hours-item.closed .hours-time {
  font-style: italic;
}

.social-links {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

.social-link {
  background: white;
  padding: 24px 16px;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  text-decoration: none;
  color: #194031;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.dark .social-link {
  background: #1f2937;
  color: white;
}

.social-link:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.social-icon {
  color: #194031;
  transition: all 0.3s ease;
}

.dark .social-icon {
  color: #D19CA4;
}

.social-text {
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

/* Estilos específicos para cada ícone de rede social */
.social-link:hover .social-icon {
  transform: scale(1.1);
}

/* Instagram - cor específica no hover */
.social-link:nth-child(1):hover .social-icon {
  color: #E4405F;
}

/* WhatsApp - cor específica no hover */
.social-link:nth-child(2):hover .social-icon {
  color: #25D366;
}

/* Telefone - cor específica no hover */
.social-link:nth-child(3):hover .social-icon {
  color: #34B7F1;
}

/* Responsive */
@media (max-width: 768px) {
  .hours-section {
    padding: 24px;
  }
  
  .social-links {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 480px) {
  .hours-section {
    padding: 20px;
  }
  
  .info-section {
    gap: 24px;
  }
  
  .social-link {
    padding: 20px 12px;
  }
}

/* Adicione isso no final do HoursAndSocial.vue */
@media screen and (max-width: 768px) {
  .info-section {
    gap: 30px;
  }
  
  .hours-section {
    padding: 24px 20px;
    border-radius: 20px;
  }
  
  .hours-title {
    font-size: 1.3rem;
  }
  
  .hours-item {
    flex-direction: column;
    gap: 4px;
    padding: 10px 0;
  }
  
  .social-links {
    grid-template-columns: repeat(3, 1fr);
    gap: 12px;
  }
  
  .social-link {
    padding: 20px 12px;
  }
}

@media screen and (max-width: 480px) {
  .info-section {
    gap: 24px;
  }
  
  .hours-section {
    padding: 20px 16px;
    border-radius: 18px;
  }
  
  .hours-title {
    font-size: 1.2rem;
    gap: 8px;
  }
  
  .hours-list {
    font-size: 0.9rem;
  }
  
  .social-links {
    grid-template-columns: 1fr;
    gap: 12px;
  }
  
  .social-link {
    padding: 18px 12px;
    flex-direction: row;
    justify-content: center;
    gap: 12px;
  }
  
  .social-text {
    font-size: 0.8rem;
  }
}

@media screen and (max-width: 360px) {
  .hours-section {
    padding: 18px 14px;
  }
  
  .hours-title {
    font-size: 1.1rem;
  }
  
  .hours-list {
    font-size: 0.85rem;
  }
  
  .social-link {
    padding: 16px 10px;
  }
}
</style>