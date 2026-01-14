<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

// Array de fotos de pets (você pode adicionar mais URLs)
const images = ref([
    'https://images.unsplash.com/photo-1507146426996-ef05306b995a?auto=format&fit=crop&w=800&q=80',
    'https://images.unsplash.com/photo-1517423440428-a5a00ad493e8?auto=format&fit=crop&w=800&q=80',
    'https://images.unsplash.com/photo-1518717758536-85ae29035b6d?auto=format&fit=crop&w=800&q=80',
    'https://images.unsplash.com/photo-1525253086316-d0c936c814f8?auto=format&fit=crop&w=800&q=80',
    'https://images.unsplash.com/photo-1508214751196-bcfd4ca60f91?auto=format&fit=crop&w=800&q=80'
]);

const currentIndex = ref(0);
const isTransitioning = ref(false);
let intervalId = null;

const intervalTime = 5000;
const transitionDuration = 1000; 

const nextImage = () => {
  if (isTransitioning.value) return;
  
  isTransitioning.value = true;
  currentIndex.value = (currentIndex.value + 1) % images.value.length;
  
  setTimeout(() => {
    isTransitioning.value = false;
  }, transitionDuration);
};

const goToImage = (index) => {
  if (isTransitioning.value || index === currentIndex.value) return;
  
  isTransitioning.value = true;
  currentIndex.value = index;
  
  setTimeout(() => {
    isTransitioning.value = false;
  }, transitionDuration);
};

const startAutoPlay = () => {
  stopAutoPlay();
  intervalId = setInterval(nextImage, intervalTime);
};

const stopAutoPlay = () => {
  if (intervalId) {
    clearInterval(intervalId);
    intervalId = null;
  }
};

const pauseOnHover = () => {
  stopAutoPlay();
};

const resumeOnLeave = () => {
  startAutoPlay();
};

onMounted(() => {
  startAutoPlay();
});

onUnmounted(() => {
  stopAutoPlay();
});
</script>

<template>
  <article 
    class="carousel" 
    @mouseenter="pauseOnHover" 
    @mouseleave="resumeOnLeave"
    aria-label="Carrossel de fotos de pets"
  >
    <div class="carousel__container">
      <div class="carousel__track" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
        <div 
          v-for="(image, index) in images" 
          :key="index" 
          class="carousel__slide"
        >
          <div 
            class="carousel__image" 
            :style="{
              'background-image': `url(${image})`,
              'animation-delay': `${index * 0.1}s`
            }"
            :class="{ 
              'carousel__image--active': index === currentIndex,
              'carousel__image--previous': index === currentIndex - 1 || (currentIndex === 0 && index === images.length - 1)
            }"
            role="img"
            :aria-label="`Foto ${index + 1} de pets`"
          >
            <div class="carousel__overlay">
              <div class="carousel__caption">
                <h3 class="carousel__title">Seu pet em boas mãos 🐾</h3>
                <p class="carousel__description">Cuidamos com amor e dedicação</p>
              </div>
            </div>
          </div>
        </div>
      </div>

     
    </div>

    <div class="carousel__indicators">
      <button 
        v-for="(image, index) in images" 
        :key="index" 
        class="carousel__indicator"
        :class="{ 'carousel__indicator--active': index === currentIndex }"
        @click="goToImage(index)"
        :aria-label="`Ir para imagem ${index + 1}`"
        :aria-current="index === currentIndex"
      >
        <span class="carousel__indicator-dot"></span>
      </button>
    </div>

  </article>
</template>

<style scoped>
.carousel {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
  border-radius: 25px;
}

.carousel__container {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.carousel__track {
  display: flex;
  height: 100%;
  transition: transform 1s cubic-bezier(0.4, 0, 0.2, 1);
}

.carousel__slide {
  flex: 0 0 100%;
  height: 100%;
  position: relative;
}

.carousel__image {
  width: 95%;
  height: 95%;
  margin: auto;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  border-radius: 25px;
  position: relative;
  transform: rotate(5deg);
  box-shadow: 
    0 20px 40px rgba(0, 0, 0, 0.2),
    0 0 0 1px rgba(255, 255, 255, 0.1),
    15px 15px 0 rgba(244, 167, 185, 0.3);
  animation: floatIn 0.8s ease-out forwards;
  opacity: 0.3;
  transition: all 1s ease;
}

.carousel__image--active {
  opacity: 1;
  transform: rotate(5deg) scale(1);
  z-index: 2;
}

.carousel__image--previous {
  opacity: 0.5;
  transform: rotate(5deg) scale(0.95);
}

@keyframes floatIn {
  from {
    opacity: 0;
    transform: rotate(10deg) translateY(20px) scale(0.95);
  }
  to {
    opacity: 1;
    transform: rotate(5deg) translateY(0) scale(1);
  }
}

.carousel__overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(to top, rgba(31, 77, 63, 0.9), transparent);
  padding: 2rem;
  border-bottom-left-radius: 25px;
  border-bottom-right-radius: 25px;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.5s ease 0.3s;
}

.carousel__image--active .carousel__overlay {
  opacity: 1;
  transform: translateY(0);
}

.carousel__caption {
  color: white;
  text-align: center;
}

.carousel__title {
  font-family: var(--font-display);
  font-size: 1.8rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.carousel__description {
  font-family: var(--font-sans);
  font-size: 1rem;
  font-weight: 400;
  opacity: 0.9;
}

/* Botões de navegação */
.carousel__button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(31, 77, 63, 0.8);
  color: white;
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
  transition: all 0.3s ease;
  backdrop-filter: blur(5px);
}

.carousel__button:hover {
  background: rgba(31, 77, 63, 1);
  transform: translateY(-50%) scale(1.1);
}

.carousel__button:active {
  transform: translateY(-50%) scale(0.95);
}

.carousel__button--prev {
  left: 1rem;
}

.carousel__button--next {
  right: 1rem;
}

.carousel__button-icon {
  font-size: 2rem;
  line-height: 1;
  font-weight: bold;
}

/* Indicadores */
.carousel__indicators {
  position: absolute;
  bottom: 1.5rem;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  gap: 0.75rem;
  z-index: 10;
}

.carousel__indicator {
  background: none;
  border: none;
  padding: 0.5rem;
  cursor: pointer;
  opacity: 0.5;
  transition: opacity 0.3s ease;
}

.carousel__indicator:hover {
  opacity: 0.8;
}

.carousel__indicator--active {
  opacity: 1;
}

.carousel__indicator-dot {
  display: block;
  width: 12px;
  height: 12px;
  background: white;
  border-radius: 50%;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  transition: transform 0.3s ease, background-color 0.3s ease;
}

.carousel__indicator--active .carousel__indicator-dot {
  background: var(--color-secondary);
  transform: scale(1.2);
}

/* Controles de play/pause */
.carousel__controls {
  position: absolute;
  top: 1rem;
  right: 1rem;
  display: flex;
  gap: 0.5rem;
  z-index: 10;
}

.carousel__control-button {
  background: rgba(31, 77, 63, 0.8);
  color: white;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  backdrop-filter: blur(5px);
}

.carousel__control-button:hover {
  background: rgba(31, 77, 63, 1);
  transform: scale(1.1);
}

.carousel__control-icon {
  font-size: 1.2rem;
}

/* Responsividade */
@media (max-width: 768px) {
  .carousel__image {
    width: 90%;
    height: 90%;
  }
  
  .carousel__button {
    width: 40px;
    height: 40px;
  }
  
  .carousel__button--prev {
    left: 0.5rem;
  }
  
  .carousel__button--next {
    right: 0.5rem;
  }
  
  .carousel__title {
    font-size: 1.4rem;
  }
  
  .carousel__overlay {
    padding: 1.5rem;
  }
}
</style>