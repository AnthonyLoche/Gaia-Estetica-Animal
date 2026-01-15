<template>
  <section class="location-section">
    <h2 class="section-title">
      <span class="material-symbols-outlined">location_on</span>
      Nossa Localização
    </h2>
    
    <p class="location-text">
      📍 <span class="location-address">{{ address }}</span>
    </p>

      <iframe
        :src="googleMapsEmbedUrl"
        width="100%"
        height="80%"
        style="border:0;"
        allowfullscreen
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade"
        title="Localização da Gaia Estética Animal"
      >
      </iframe>
  </section>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  address: {
    type: String,
    default: 'Rua dos Cravos, 181 – Guanabara, Joinville – SC'
  },
  googleMapsLink: {
    type: String,
    default: 'https://maps.google.com'
  },
  googleMapsEmbedUrl: {
    type: String,
    default: 'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3579.3444073101097!2d-48.8766285!3d-26.2165!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x94deaf2b9e7e3c1f%3A0xfc6c9a8c8e0a3a1a!2sR.%20dos%20Cravos%2C%20181%20-%20Guanabara%2C%20Joinville%20-%20SC%2C%2089207-740!5e0!3m2!1spt-BR!2sbr!4v1644337400000!5m2!1spt-BR!2sbr'
  }
})

const googleMapsEmbedUrl = computed(() => {
  if (props.googleMapsEmbedUrl) return props.googleMapsEmbedUrl
  
  const encodedAddress = encodeURIComponent(props.address)
  return `https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3579.3444073101097!2d-48.8766285!3d-26.2165!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x94deaf2b9e7e3c1f%3A0xfc6c9a8c8e0a3a1a!2s${encodedAddress}!5e0!3m2!1spt-BR!2sbr!4v1644337400000!5m2!1spt-BR!2sbr`
})
</script>

<style scoped>
.location-section {
  background: rgba(255, 255, 255, 0.5);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 24px;
  padding: 32px;
  box-shadow: 0 20px 40px rgba(25, 64, 49, 0.05);
  height: 700px;

}

.dark .location-section {
  background: rgba(31, 41, 55, 0.4);
  border-color: rgba(55, 65, 81, 0.3);
}

.section-title {
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 24px;
  display: flex;
  align-items: center;
  gap: 12px;
  color: #194031;
}

.dark .section-title {
  color: #D19CA4;
}

.section-title .material-symbols-outlined {
  font-size: 28px;
}

.location-text {
  font-size: 1.125rem;
  line-height: 1.6;
  margin-bottom: 24px;
}

.location-address {
  font-weight: 600;
}

.map-container {
  position: relative;
  border-radius: 20px;
  overflow: hidden;
  background: #f3f4f6;
  /* aspect-ratio: 16/9; */
  min-height: 400px;
}

.dark .map-container {
  background: #111827;
}

.map-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: none;
  z-index: 1;
}

.map-marker {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
  pointer-events: none;
}

.marker-icon {
  font-size: 48px;
  color: #194031;
  animation: bounce 2s infinite;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.3));
}

.dark .marker-icon {
  color: #D19CA4;
}

.marker-shadow {
  position: absolute;
  bottom: -4px;
  left: 50%;
  transform: translateX(-50%);
  width: 20px;
  height: 4px;
  background: rgba(0, 0, 0, 0.2);
  border-radius: 50%;
}

.map-link {
  position: absolute;
  bottom: 20px;
  right: 20px;
  background: white;
  padding: 12px 20px;
  border-radius: 12px;
  font-weight: 700;
  font-size: 0.875rem;
  text-decoration: none;
  color: #194031;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
  transition: all 0.3s ease;
  z-index: 3;
}

.dark .map-link {
  background: #1f2937;
  color: white;
}

.map-link:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 25px rgba(0, 0, 0, 0.3);
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translate(-50%, -50%);
  }
  40% {
    transform: translate(-50%, -60%);
  }
  60% {
    transform: translate(-50%, -55%);
  }
}

/* Responsive */
@media (max-width: 768px) {
  .location-section {
    padding: 24px;
  }
  
  .section-title {
    font-size: 1.5rem;
  }
  
  .map-container {
    min-height: 350px;
  }
}

@media (max-width: 480px) {
  .location-section {
    padding: 20px;
  }
  
  .map-container {
    min-height: 300px;
  }
  
  .map-link {
    padding: 10px 16px;
    font-size: 0.75rem;
    bottom: 15px;
    right: 15px;
  }
}

/* Adicione isso no LocationMap.vue se existir */
@media screen and (max-width: 480px) {
  .location-section {
    padding: 20px 16px;
  }
  
  .section-title {
    font-size: 1.4rem;
  }
  
  .location-text {
    font-size: 1rem;
  }
  
  .map-container {
    aspect-ratio: 4/3; /* Mais quadrado em mobile */
    min-height: 300px;
  }
  
  .map-link {
    padding: 10px 16px;
    font-size: 0.75rem;
    bottom: 15px;
    right: 15px;
  }
}

@media screen and (max-width: 360px) {
  .location-section {
    padding: 16px 12px;
  }
  
  .section-title {
    font-size: 1.2rem;
  }
  
  .map-link {
    padding: 8px 12px;
    bottom: 10px;
    right: 10px;
  }
}
</style>