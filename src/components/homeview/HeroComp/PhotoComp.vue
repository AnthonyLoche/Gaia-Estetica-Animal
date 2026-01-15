<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { dogPhotos } from '@/data/images';


const images = ref([]);
const currentIndex = ref(0);
const isTransitioning = ref(false);

let intervalId = null;

const intervalTime = 5000;
const transitionDuration = 1000;

/* Embaralha o array (Fisher-Yates) */
const shuffleArray = (array) => {
  const shuffled = [...array];
  for (let i = shuffled.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
  }
  return shuffled;
};

/* Seleciona 6 imagens aleatórias */
const selectRandomImages = () => {
  images.value = shuffleArray(dogPhotos).slice(0, 6);
};

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

onMounted(() => {
  selectRandomImages(); // Escolhe 6 novas imagens
  startAutoPlay();
});

onUnmounted(stopAutoPlay);
</script>


<template>
  <article
    class="carousel"
    @mouseenter="stopAutoPlay"
    @mouseleave="startAutoPlay"
  >
    <div class="carousel__container">
      <div
        class="carousel__track"
        :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
      >
        <div
          v-for="(image, index) in images"
          :key="index"
          class="carousel__slide"
        >
          <div
            class="carousel__image"
            :style="{ backgroundImage: `url(${image})` }"
            :class="{ 'carousel__image--active': index === currentIndex }"
          >
            <div class="carousel__overlay">
              <h3 class="carousel__title">Seu pet em boas mãos 🐾</h3>
              <p class="carousel__description">
                Cuidamos com amor e dedicação
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="carousel__indicators">
      <button
        v-for="(_, index) in images"
        :key="index"
        class="carousel__indicator"
        :class="{ active: index === currentIndex }"
        @click="goToImage(index)"
      />
    </div>
  </article>
</template>

<style scoped>
.carousel {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: visible; 
}

.carousel__container {
  width: 100%;
  height: 100%;
  overflow: hidden; 
}

.carousel__track {
  display: flex;
  height: 100%;
  transition: transform 1s ease;
}

.carousel__slide {
  flex: 0 0 100%;
  height: 100%;
  padding: 40px; /* espaço para rotação */
  box-sizing: border-box;
}

.carousel__image {
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  border-radius: 25px;
  transform: rotate(5deg);
  transition: all 1s ease;
  position: relative;
}

.carousel__image--active {
  transform: rotate(5deg) scale(1);
}

.carousel__overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 2rem;
  background: linear-gradient(to top, rgba(31, 77, 63, 0.9), transparent);
  border-radius: 0 0 25px 25px;
  color: white;
  text-align: center;
}

.carousel__title {
  font-size: 1.6rem;
  font-weight: 700;
}

.carousel__description {
  font-size: 1rem;
  opacity: 0.9;
}

.carousel__indicators {
  position: absolute;
  bottom: 1.5rem;
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 10px;
}

.carousel__indicator {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: none;
  background: white;
  opacity: 0.5;
  cursor: pointer;
}

.carousel__indicator.active {
  opacity: 1;
  background: var(--color-secondary);
}

/* MOBILE */
@media (max-width: 1024px) {
  .carousel {
    min-height: 350px;
  }

  .carousel__image {
    min-height: 300px;
    transform: rotate(3deg);
  }
}
</style>
