<template>
  <section class="gallery-carousel-section">
    <div class="container">
      <div class="gallery-header">
        <div>
          <h3 class="section-title">Nosso Ambiente</h3>
          <p>Um espaço projetado para ser acolhedor, limpo e seguro para todos os tamanhos e raças.</p>
        </div>
      </div>
      
      <!-- Carrossel de Fotos -->
      <div class="carousel-wrapper" ref="carouselWrapper">
        <!-- Container do Carrossel -->
        <div 
          class="carousel-container" 
          ref="carouselContainer"
          @click="openLightbox"
        >
          <div class="carousel-track" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
            <div 
              v-for="(image, index) in galleryImages" 
              :key="image.id"
              class="carousel-slide"
              :class="{ 'active': currentIndex === index }"
            >
              <div class="slide-content">
                <img 
                  :src="image.src" 
                  :alt="image.alt"
                  :loading="index < 2 ? 'eager' : 'lazy'"
                  class="carousel-image"
                  @load="handleImageLoad"
                />
                <div class="image-overlay">
                  <div class="image-info">
                    <span class="image-number">{{ index + 1 }} / {{ galleryImages.length }}</span>
                    <p class="image-description">{{ image.description }}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Botões de navegação dentro do carrossel -->
          <button 
            class="carousel-btn carousel-btn-prev" 
            @click.stop="prevImage"
            :aria-disabled="currentIndex === 0"
            aria-label="Foto anterior"
          >
            <ChevronLeft :size="24" fillColor="white" />
          </button>
          
          <button 
            class="carousel-btn carousel-btn-next" 
            @click.stop="nextImage"
            :aria-disabled="currentIndex === galleryImages.length - 1"
            aria-label="Próxima foto"
          >
            <ChevronRight :size="24" fillColor="white" />
          </button>
          
          <!-- Indicadores -->
          <div class="indicators">
            <button 
              v-for="(image, index) in galleryImages" 
              :key="`indicator-${image.id}`"
              class="indicator"
              :class="{ 'active': currentIndex === index }"
              @click.stop="goToImage(index)"
              :aria-label="`Ir para foto ${index + 1}`"
            >
              <div class="indicator-dot"></div>
            </button>
          </div>
          

          <button 
            class="fullscreen-btn-inner" 
            @click.stop="toggleFullscreen"
            :aria-label="isFullscreen ? 'Sair do modo tela cheia' : 'Expandir para tela cheia'"
          >
            <Fullscreen v-if="!isFullscreen" :size="20" fillColor="white" />
            <FullscreenExit v-else :size="20" fillColor="white" />
          </button>
        </div>
      </div>
      
      <!-- Lightbox Modal -->
      <div v-if="showLightbox" class="lightbox" @click="closeLightbox">
        <div class="lightbox-content" @click.stop>
          <!-- Botão fechar -->
          <button class="lightbox-close" @click="closeLightbox" aria-label="Fechar visualização">
            <Close :size="24" fillColor="white" />
          </button>
          
          <!-- Imagem ampliada -->
          <div class="lightbox-image-container">
            <img 
              :src="currentImage.src" 
              :alt="currentImage.alt"
              class="lightbox-image"
              @load="handleLightboxImageLoad"
            />
            <div class="lightbox-info">
              <h3 class="lightbox-title">{{ currentImage.alt }}</h3>
              <p class="lightbox-description">{{ currentImage.description }}</p>
              <div class="lightbox-counter">
                {{ currentIndex + 1 }} / {{ galleryImages.length }}
              </div>
            </div>
          </div>
          
          <!-- Botões de navegação no lightbox -->
          <button 
            class="lightbox-btn lightbox-prev" 
            @click.stop="prevImage"
            :aria-disabled="currentIndex === 0"
            aria-label="Foto anterior"
          >
            <ChevronLeft :size="32" fillColor="white" />
          </button>
          
          <button 
            class="lightbox-btn lightbox-next" 
            @click.stop="nextImage"
            :aria-disabled="currentIndex === galleryImages.length - 1"
            aria-label="Próxima foto"
          >
            <ChevronRight :size="32" fillColor="white" />
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import ChevronLeft from 'vue-material-design-icons/ChevronLeft.vue';
import ChevronRight from 'vue-material-design-icons/ChevronRight.vue';
import Fullscreen from 'vue-material-design-icons/Fullscreen.vue';
import FullscreenExit from 'vue-material-design-icons/FullscreenExit.vue';
import Close from 'vue-material-design-icons/Close.vue';

const galleryImages = ref([
  {
    id: 1,
    src: 'https://images.unsplash.com/photo-1596462502278-27bfdc403348?ixlib=rb-4.0.3&auto=format&fit=crop&w=1000&q=80',
    alt: 'Cão no banho em petshop real',
    description: 'Banho profissional com equipamentos adequados'
  },
  {
    id: 2,
    src: 'https://images.unsplash.com/photo-1560743641-3914f2c45636?ixlib=rb-4.0.3&auto=format&fit=crop&w=1000&q=80',
    alt: 'Sala de tosa profissional',
    description: 'Estação de tosa completa e higienizada'
  },
  {
    id: 3,
    src: 'https://images.unsplash.com/photo-1559599101-f09722fb4948?ixlib=rb-4.0.3&auto=format&fit=crop&w=1000&q=80',
    alt: 'Tosador profissional em ação',
    description: 'Tosador especializado realizando corte'
  },
  {
    id: 4,
    src: 'https://images.unsplash.com/photo-1623387641168-d9803ddd3f35?ixlib=rb-4.0.3&auto=format&fit=crop&w=1000&q=80',
    alt: 'Procedimento de higiene',
    description: 'Limpeza de ouvidos e cuidados especiais'
  },
  {
    id: 5,
    src: 'https://images.unsplash.com/photo-1516734212186-a967f81ad0d7?ixlib=rb-4.0.3&auto=format&fit=crop&w=1000&q=80',
    alt: 'Interior de petshop moderno',
    description: 'Ambiente climatizado e equipado'
  },
  {
    id: 6,
    src: 'https://images.unsplash.com/photo-1596273315327-946fdd6cac15?ixlib=rb-4.0.3&auto=format&fit=crop&w=1000&q=80',
    alt: 'Cão sendo secado',
    description: 'Secagem com capas térmicas'
  },
  {
    id: 7,
    src: 'https://images.unsplash.com/photo-1548199973-03cce0bbc87b?ixlib=rb-4.0.3&auto=format&fit=crop&w=1000&q=80',
    alt: 'Sala de banho individual',
    description: 'Boxes individuais para conforto e segurança'
  },
  {
    id: 8,
    src: 'https://images.unsplash.com/photo-1596492784531-6e6eb5ea9993?ixlib=rb-4.0.3&auto=format&fit=crop&w=1000&q=80',
    alt: 'Produtos de petshop',
    description: 'Variedade de produtos profissionais'
  }
]);

// Estado do carrossel
const currentIndex = ref(0);
const showLightbox = ref(false);
const isFullscreen = ref(false);
const isPlaying = ref(true);
const autoplayInterval = ref(null);
const carouselContainer = ref(null);
const carouselWrapper = ref(null);
const timerDuration = 4000; // 4 segundos por imagem

// Computed
const currentImage = computed(() => galleryImages.value[currentIndex.value]);

// Navegação
const nextImage = () => {
  if (currentIndex.value < galleryImages.value.length - 1) {
    currentIndex.value++;
  } else {
    currentIndex.value = 0;
  }
  resetAutoplay();
};

const prevImage = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--;
  } else {
    currentIndex.value = galleryImages.value.length - 1;
  }
  resetAutoplay();
};

const goToImage = (index) => {
  currentIndex.value = index;
  resetAutoplay();
};

// Autoplay
const startAutoplay = () => {
  if (autoplayInterval.value) {
    clearInterval(autoplayInterval.value);
  }
  autoplayInterval.value = setInterval(() => {
    nextImage();
  }, timerDuration);
};

const stopAutoplay = () => {
  if (autoplayInterval.value) {
    clearInterval(autoplayInterval.value);
    autoplayInterval.value = null;
  }
};

const resetAutoplay = () => {
  if (isPlaying.value && !showLightbox.value) {
    stopAutoplay();
    startAutoplay();
  }
};

const toggleAutoplay = () => {
  isPlaying.value = !isPlaying.value;
  if (isPlaying.value && !showLightbox.value) {
    startAutoplay();
  } else {
    stopAutoplay();
  }
};

// Lightbox
const openLightbox = (event) => {
  // Verifica se o clique não foi em um botão
  if (!event.target.closest('button')) {
    showLightbox.value = true;
    stopAutoplay(); // Pausa autoplay quando lightbox está aberto
  }
};

const closeLightbox = () => {
  showLightbox.value = false;
  if (isPlaying.value) {
    startAutoplay(); // Retoma autoplay quando lightbox fecha
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
const handleImageLoad = () => {
  // Imagem carregada
};

const handleLightboxImageLoad = () => {
};

const handleKeydown = (event) => {
  if (showLightbox.value) {
    switch(event.key) {
      case 'ArrowLeft':
        prevImage();
        break;
      case 'ArrowRight':
        nextImage();
        break;
      case 'Escape':
        closeLightbox();
        break;
      case ' ':
      case 'Spacebar':
        event.preventDefault();
        toggleAutoplay();
        break;
    }
  } else {
    switch(event.key) {
      case 'ArrowLeft':
        prevImage();
        break;
      case 'ArrowRight':
        nextImage();
        break;
      case 'Enter':
      case ' ':
        openLightbox({ target: { closest: () => false } });
        break;
    }
  }
};

// Fullscreen change listener
const handleFullscreenChange = () => {
  isFullscreen.value = !!document.fullscreenElement;
};

// Lifecycle hooks
onMounted(() => {
  startAutoplay();
  window.addEventListener('keydown', handleKeydown);
  document.addEventListener('fullscreenchange', handleFullscreenChange);
});

onUnmounted(() => {
  stopAutoplay();
  window.removeEventListener('keydown', handleKeydown);
  document.removeEventListener('fullscreenchange', handleFullscreenChange);
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

.gallery-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #194031;
  font-weight: 700;
  background: none;
  border: none;
  border-bottom: 2px solid #194031;
  padding-bottom: 0.25rem;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: 1rem;
}

.dark .gallery-btn {
  color: #F2EBC4;
  border-bottom-color: #F2EBC4;
}

.gallery-btn:hover {
  color: #E8A8B1;
  border-bottom-color: #E8A8B1;
}

.gallery-btn:hover .gallery-btn-icon {
  transform: translateX(4px);
}

.gallery-btn-icon {
  transition: transform 0.3s ease;
}

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
  cursor: pointer;
  transition: all 0.3s ease;
}

.dark .carousel-container {
  background: #0D1F18;
}

.carousel-container:hover {
  box-shadow: 0 30px 60px rgba(0, 0, 0, 0.25);
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

.slide-content {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
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

.image-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent 70%);
  padding: 2rem;
  opacity: 0;
  transition: opacity 0.3s ease;
  z-index: 2;
}

.carousel-container:hover .image-overlay {
  opacity: 1;
}

.image-info {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  max-width: 800px;
  margin: 0 auto;
}

.image-number {
  font-size: 0.875rem;
  color: rgba(255, 255, 255, 0.9);
  font-weight: 600;
  letter-spacing: 0.5px;
}

.image-description {
  color: white;
  font-size: 1.125rem;
  font-weight: 500;
  margin: 0;
  line-height: 1.4;
}

/* Botões de navegação dentro do carrossel */
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

.carousel-btn:hover:not(:disabled) {
  background: rgba(232, 168, 177, 0.8);
  border-color: white;
  transform: translateY(-50%) scale(1.1);
}

.carousel-btn:active:not(:disabled) {
  transform: translateY(-50%) scale(0.95);
}

.carousel-btn:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}

span{
    display: flex;
    align-items: center;
    justify-content: center;
}

.carousel-btn-prev {
  left: 2rem;
}

.carousel-btn-next {
  right: 2rem;
}

/* Indicadores */
.indicators {
  position: absolute;
  bottom: 1rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 0.75rem;
  z-index: 10;
  background: rgba(0, 0, 0, 0.5);
  padding: 0.25rem 0.25rem;
  border-radius: 50px;
  backdrop-filter: blur(10px);
}

.indicator {
  background: none;
  border: none;
  padding: 0.5rem;
  cursor: pointer;
  opacity: 0.5;
  transition: opacity 0.3s ease;
}

.indicator:hover {
  opacity: 0.8;
}

.indicator.active {
  opacity: 1;
}

.indicator-dot {
  width: 12px;
  height: 12px;
  background-color: white;
  border-radius: 50%;
  transition: transform 0.3s ease, background-color 0.3s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.indicator.active .indicator-dot {
  transform: scale(1.3);
  background-color: #E8A8B1;
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

.counter-divider {
  opacity: 0.7;
}

.total-number {
  opacity: 0.8;
}

/* Botão Fullscreen dentro do carrossel */
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

/* Lightbox */
.lightbox {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.95);
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.lightbox-content {
  position: relative;
  width: 95%;
  max-width: 1200px;
  height: 90vh;
  background: #000;
  border-radius: 1rem;
  overflow: hidden;
  animation: scaleIn 0.3s ease;
}

@keyframes scaleIn {
  from {
    transform: scale(0.9);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

.lightbox-close {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 10;
  backdrop-filter: blur(5px);
}

.lightbox-close:hover {
  background: rgba(232, 168, 177, 0.8);
  transform: scale(1.1);
}

.lightbox-image-container {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}

.lightbox-image {
  width: 100%;
  height: 85%;
  object-fit: contain;
  background: #000;
}

.lightbox-info {
  height: 15%;
  background: rgba(0, 0, 0, 0.8);
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 0.5rem;
}

.lightbox-title {
  color: white;
  font-size: 1.5rem;
  font-weight: 600;
  margin: 0;
}

.lightbox-description {
  color: rgba(255, 255, 255, 0.8);
  font-size: 1rem;
  margin: 0;
}

.lightbox-counter {
  color: #E8A8B1;
  font-size: 0.875rem;
  font-weight: 600;
}

.lightbox-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.5);
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  width: 64px;
  height: 64px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 10;
  backdrop-filter: blur(5px);
}

.lightbox-btn:hover:not(:disabled) {
  background: rgba(232, 168, 177, 0.8);
  border-color: white;
  transform: translateY(-50%) scale(1.1);
}

.lightbox-btn:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}

.lightbox-prev {
  left: 2rem;
}

.lightbox-next {
  right: 2rem;
}

.lightbox-download {
  position: absolute;
  bottom: 2rem;
  right: 2rem;
  background: rgba(232, 168, 177, 0.8);
  border: none;
  border-radius: 12px;
  padding: 0.75rem 1.5rem;
  color: white;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 10;
}

.lightbox-download:hover {
  background: #E8A8B1;
  transform: translateY(-2px);
}

/* Responsividade */
@media (max-width: 1200px) {
  .carousel-container {
    height: 600px;
  }
}

@media (max-width: 992px) {
  .carousel-container {
    height: 500px;
  }
  
  .section-title {
    font-size: 2.25rem;
  }
}

@media (max-width: 768px) {
  .gallery-carousel-section {
    padding: 4rem 0;
  }
  
  .carousel-container {
    height: 400px;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .carousel-btn {
    width: 48px;
    height: 48px;
  }
  
  .lightbox-content {
    height: 80vh;
  }
  
  .lightbox-btn {
    width: 48px;
    height: 48px;
  }
}

@media (max-width: 640px) {
  .gallery-carousel-section {
    padding: 3rem 0;
  }
  
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
  
  .section-title {
    font-size: 1.75rem;
  }
  
  .gallery-header {
    text-align: center;
    align-items: center;
    gap: 1rem;
  }
  
  .indicators {
    padding: 0.5rem 0.75rem;
    gap: 0.5rem;
  }
  
  .image-counter {
    top: 1rem;
    right: 1rem;
    font-size: 0.75rem;
    padding: 0.375rem 0.75rem;
  }
  
  .fullscreen-btn-inner {
    top: 1rem;
    left: 1rem;
  }
  
  .lightbox-content {
    width: 100%;
    height: 100%;
    border-radius: 0;
  }
  
  .lightbox-close {
    top: 1rem;
    right: 1rem;
  }
  
  .lightbox-btn {
    width: 40px;
    height: 40px;
  }
  
  .lightbox-prev {
    left: 1rem;
  }
  
  .lightbox-next {
    right: 1rem;
  }
}

/* Fullscreen styles */
:fullscreen .carousel-container {
  width: 100%;
  height: 100vh;
  border-radius: 0;
  max-width: none;
}

/* Acessibilidade */
.carousel-btn:focus,
.gallery-btn:focus,
.indicator:focus,
.fullscreen-btn-inner:focus,
.lightbox-close:focus,
.lightbox-btn:focus,
.lightbox-download:focus {
  outline: 2px solid #E8A8B1;
  outline-offset: 2px;
}

@media (prefers-reduced-motion: reduce) {
  .carousel-track,
  .carousel-image,
  .carousel-btn,
  .indicator-dot,
  .image-overlay,
  .lightbox,
  .lightbox-content {
    transition: none;
    animation: none;
  }
}

/* Loading state */
.carousel-image {
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: loading 1.5s infinite;
}

@keyframes loading {
  0% {
    background-position: 200% 0;
  }
  100% {
    background-position: -200% 0;
  }
}

.carousel-image.loaded {
  background: none;
  animation: none;
}
</style>