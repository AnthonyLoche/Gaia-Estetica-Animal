<template>
  <div>
    <HeaderMain />

    <div class="contact-page">
      <div class="contact-container">
        
        <!-- Header -->
        <header
          class="contact-header section-animate"
          data-animate="fade-up"
        >
          <h1 class="contact-title">
            Fale Conosco e Venha nos Visitar!
          </h1>

          <p class="contact-subtitle">
            Estamos prontos para cuidar do seu pet com todo carinho e profissionalismo que ele merece.
          </p>
        </header>

        <!-- Main Content -->
        <div class="contact-content">
          
          <!-- Form -->
          <section
            class="section-animate"
            data-animate="fade-right"
          >
            <ContactForm @form-submitted="handleFormSubmission" />
          </section>

          <!-- Info -->
          <section
            class="info-section section-animate"
            data-animate="fade-left"
          >
            <LocationMap 
              :address="location.address"
              :google-maps-link="location.googleMapsLink"
              :map-image="location.mapImage"
            />

            <HoursAndSocial />
          </section>

        </div>
      </div>
    </div>

    <FooterMain />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { HeaderMain, FooterMain, ContactForm, LocationMap, HoursAndSocial } from '@/components'

// Location data
const location = ref({
  address: 'Rua dos Cravos, 181 – Guanabara, Joinville – SC',
  googleMapsLink: 'https://maps.google.com',
  mapImage:
    'https://lh3.googleusercontent.com/aida-public/AB6AXuDKn756EzHIw9-rDrFNi-wlzhU9ubWLJcu4Q1KIYlXH7chsRiYCmvtmve8nQkO7h7i2wJDPPRKviDnJnKjSFBbANvDIOkoVEEcACGyGVf6oGawefHRx7w5g9yXDy61ET0uV160cAuY5g-sBh6k3EB7Y5Xjt4-JLbn3-OlgZU0oeW3VBMMCBHKt8CfFogvOCEw3sm48nNQy4epDx5b3UIXrr2V1gKPp-5glMk8gmRihY0ZOJy2NVe5tc76rJe7A6o8zOHx77fPspiw'
})

const handleFormSubmission = (formData) => {
  console.log('Form data received in parent:', formData)
}

/* ===============================
   Intersection Observer
================================ */
const initIntersectionObservers = () => {
  const observer = new IntersectionObserver(
    entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('animate-in')
        }
      })
    },
    { threshold: 0.1 }
  )

  document
    .querySelectorAll('[data-animate]')
    .forEach(el => observer.observe(el))

  return observer
}

onMounted(() => {
  const observer = initIntersectionObservers()
  onUnmounted(() => observer.disconnect())
})
</script>

<style scoped>
/* ===============================
   PAGE BASE
================================ */
.contact-page {
  min-height: 100vh;
  color: #194031;
  font-family: 'Lexend', 'Segoe UI', sans-serif;
}

.contact-container {
  width: 90%;
  margin: 0 auto;
  padding: 0 20px;
  overflow-x: hidden;
}

/* ===============================
   HEADER
================================ */
.contact-header {
  text-align: center;
  padding: 60px 0 40px;
  max-width: 800px;
  margin: 0 auto;
}

.contact-title {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

.contact-subtitle {
  font-size: 1.125rem;
  line-height: 1.6;
  color: rgba(25, 64, 49, 0.8);
}

/* ===============================
   CONTENT
================================ */
.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  padding-bottom: 60px;
}

.info-section {
  display: flex;
  flex-direction: column;
  gap: 40px;
}

/* ===============================
   ANIMATIONS
================================ */
.section-animate {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.7s ease, transform 0.7s ease;
  height: 100%;
}

.section-animate[data-animate="fade-up"] {
  transform: translateY(40px);
}

.section-animate[data-animate="fade-left"] {
  transform: translateX(40px);
}

.section-animate[data-animate="fade-right"] {
  transform: translateX(-40px);
}

.section-animate.animate-in {
  opacity: 1;
  transform: translate(0, 0);
}

/* ===============================
   RESPONSIVE
================================ */
@media (max-width: 1024px) {
  .contact-content {
    grid-template-columns: 1fr;
  }

  .contact-title {
    font-size: 2.5rem;
  }
}

@media (max-width: 768px) {
  .contact-title {
    font-size: 2.2rem;
  }

  .contact-subtitle {
    font-size: 1rem;
  }
}

@media (max-width: 480px) {
  .contact-title {
    font-size: 1.8rem;
  }
}
</style>
