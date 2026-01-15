<template>
  <section class="gallery-carousel-section">
    <div class="container">
      <div class="gallery-header">
        <div>
          <h3 class="section-title">Nosso Ambiente</h3>
          <p>
            Um espaço projetado para ser acolhedor, limpo e seguro para todos os
            tamanhos e raças.
          </p>
        </div>
      </div>

      <!-- Carrossel -->
      <div class="carousel-wrapper">
        <div
          class="carousel-container"
          ref="carouselContainer"
        >
          <div
            class="carousel-track"
            :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
          >
            <div
              v-for="(image, index) in galleryImages"
              :key="index"
              class="carousel-slide"
              :class="{ active: currentIndex === index }"
            >
              <img
                :src="image"
                class="carousel-image"
                :loading="index < 2 ? 'eager' : 'lazy'"
                @load="handleImageLoad"
              />
            </div>
          </div>

          <!-- Navegação -->
          <button class="carousel-btn carousel-btn-prev" @click.stop="prevImage">
            <ChevronLeft :size="24" fillColor="white" />
          </button>

          <button class="carousel-btn carousel-btn-next" @click.stop="nextImage">
            <ChevronRight :size="24" fillColor="white" />
          </button>

          <!-- Contador -->
          <div class="image-counter">
            <span class="current-number">{{ currentIndex + 1 }}</span>
            <span class="counter-divider">/</span>
            <span class="total-number">{{ galleryImages.length }}</span>
          </div>

          <!-- Fullscreen -->
          <button class="fullscreen-btn-inner" @click.stop="toggleFullscreen">
            <Fullscreen v-if="!isFullscreen" :size="20" fillColor="white" />
            <FullscreenExit v-else :size="20" fillColor="white" />
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

import ChevronLeft from 'vue-material-design-icons/ChevronLeft.vue';
import ChevronRight from 'vue-material-design-icons/ChevronRight.vue';
import Fullscreen from 'vue-material-design-icons/Fullscreen.vue';
import FullscreenExit from 'vue-material-design-icons/FullscreenExit.vue';

import { dogPhotos } from '@/data/images';

// State
const galleryImages = ref([]);
const currentIndex = ref(0);
const isFullscreen = ref(false);
const autoplayInterval = ref(null);
const carouselContainer = ref(null);
const loadedImages = ref([]);

const timerDuration = 4000;

// Navigation
const nextImage = () => {
  currentIndex.value =
    (currentIndex.value + 1) % galleryImages.value.length;
};

const prevImage = () => {
  currentIndex.value =
    (currentIndex.value - 1 + galleryImages.value.length) %
    galleryImages.value.length;
};

// Autoplay
const startAutoplay = () => {
  stopAutoplay();
  autoplayInterval.value = setInterval(nextImage, timerDuration);
};

const stopAutoplay = () => {
  if (autoplayInterval.value) {
    clearInterval(autoplayInterval.value);
    autoplayInterval.value = null;
  }
};

// Fullscreen
const toggleFullscreen = () => {
  if (!document.fullscreenElement) {
    carouselContainer.value?.requestFullscreen?.();
    isFullscreen.value = true;
  } else {
    document.exitFullscreen?.();
    isFullscreen.value = false;
  }
};

// Image loading
const handleImageLoad = (event) => {
  event.target.classList.add('loaded');
  const index = Array.from(event.target.parentNode.parentNode.children)
    .indexOf(event.target.parentNode);
  loadedImages.value[index] = true;
};

// Keyboard navigation (apenas para navegação no carrossel)
const handleKeyDown = (event) => {
  switch(event.key) {
    case 'ArrowLeft':
      event.preventDefault();
      prevImage();
      break;
    case 'ArrowRight':
      event.preventDefault();
      nextImage();
      break;
  }
};

// Lifecycle
onMounted(() => {
  // Usa TODAS as fotos do dogPhotos
  galleryImages.value = [...dogPhotos];
  
  // Inicia carregamento das primeiras imagens
  loadedImages.value = new Array(galleryImages.value.length).fill(false);
  
  startAutoplay();
  
  // Adiciona listener para teclado
  document.addEventListener('keydown', handleKeyDown);
});

onUnmounted(() => {
  stopAutoplay();
  document.removeEventListener('keydown', handleKeyDown);
});
</script>

<style scoped>
.gallery-carousel-section {
  padding: 2rem 0;
  width: 100%;
}

.container {
  width: 95%;
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 20px;
}

.gallery-header {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 3rem;
  gap: 1.5rem;
}

@media (min-width: 768px) {
  .gallery-header {
    flex-direction: row;
    align-items: flex-end;
  }
}

.gallery-header div {
  max-width: 36rem;
}

.section-title {
  font-family: var(--font-display, 'Playfair Display'), serif;
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: #194031;
}

.dark .section-title {
  color: #F2EBC4;
}

.gallery-header p {
  color: rgba(25, 64, 49, 0.8);
  font-size: 1.125rem;
  line-height: 1.6;
}

.dark .gallery-header p {
  color: rgba(242, 235, 196, 0.8);
}

/* Carrossel */
.carousel-wrapper {
  position: relative;
  width: 100%;
  margin-bottom: 2rem;
}

.carousel-container {
  position: relative;
  width: 100%;
  height: 700px;
  overflow: hidden;
  border-radius: 1.5rem;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.2);
  background: #F2EBC4;
  transition: all 0.3s ease;
}

.dark .carousel-container {
  background: #0D1F18;
}

.carousel-track {
  display: flex;
  transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);
  height: 100%;
}

.carousel-slide {
  flex: 0 0 100%;
  height: 100%;
  position: relative;
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.8s ease;
}

.carousel-slide.active .carousel-image {
  transform: scale(1.02);
}

/* Botões do carrossel */
.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.5);
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  width: 56px;
  height: 56px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  color: white;
  z-index: 10;
  backdrop-filter: blur(5px);
}

.carousel-btn:hover {
  background: rgba(232, 168, 177, 0.8);
  border-color: white;
  transform: translateY(-50%) scale(1.1);
}

.carousel-btn-prev {
  left: 2rem;
}

.carousel-btn-next {
  right: 2rem;
}

/* Contador */
.image-counter {
  position: absolute;
  top: 2rem;
  right: 2rem;
  background: rgba(0, 0, 0, 0.6);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.875rem;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 0.25rem;
  z-index: 10;
  backdrop-filter: blur(5px);
}

.current-number {
  color: #E8A8B1;
  font-size: 1.125rem;
}

/* Fullscreen button */
.fullscreen-btn-inner {
  position: absolute;
  top: 2rem;
  left: 2rem;
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 12px;
  padding: 0.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  color: white;
  z-index: 10;
  backdrop-filter: blur(5px);
}

.fullscreen-btn-inner:hover {
  background: rgba(232, 168, 177, 0.8);
  border-color: white;
  transform: scale(1.1);
}

/* Responsividade do carrossel */
@media (max-width: 1200px) {
  .carousel-container {
    height: 600px;
  }
}

@media (max-width: 992px) {
  .carousel-container {
    height: 500px;
  }
}

@media (max-width: 768px) {
  .carousel-container {
    height: 400px;
  }
}

@media (max-width: 640px) {
  .carousel-container {
    height: 350px;
  }
  
  .carousel-btn {
    width: 40px;
    height: 40px;
  }
  
  .carousel-btn-prev {
    left: 1rem;
  }
  
  .carousel-btn-next {
    right: 1rem;
  }
  
  .image-counter {
    top: 1rem;
    right: 1rem;
    padding: 0.4rem 0.8rem;
    font-size: 0.8rem;
  }
  
  .current-number {
    font-size: 1rem;
  }
  
  .fullscreen-btn-inner {
    top: 1rem;
    left: 1rem;
    padding: 0.4rem;
  }
}

@media (max-width: 480px) {
  .carousel-container {
    height: 300px;
  }
  
  .gallery-header {
    margin-bottom: 2rem;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .gallery-header p {
    font-size: 1rem;
  }
}

/* Animações de loading */
.carousel-image:not(.loaded) {
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: loading 1.5s infinite;
}

@keyframes loading {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}

/* Estilos para fullscreen */
:fullscreen .carousel-container {
  border-radius: 0;
  height: 100vh;
  height: 100dvh;
  cursor: default;
}

:fullscreen .carousel-slide.active .carousel-image {
  transform: scale(1);
}

/* Ajusta botões em modo fullscreen */
:fullscreen .carousel-btn {
  width: 64px;
  height: 64px;
}

:fullscreen .carousel-btn-prev {
  left: 3rem;
}

:fullscreen .carousel-btn-next {
  right: 3rem;
}

:fullscreen .image-counter {
  top: 3rem;
  right: 3rem;
  font-size: 1rem;
  padding: 0.75rem 1.5rem;
}

:fullscreen .current-number {
  font-size: 1.25rem;
}

:fullscreen .fullscreen-btn-inner {
  top: 3rem;
  left: 3rem;
  padding: 0.75rem;
}
</style>