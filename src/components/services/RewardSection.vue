<template>
  <div class="page-wrapper">
    <div class="hero-banner">
      <div class="hero-content">
        <h1 class="hero-title">
          Dê ao seu pet o cuidado que ele merece
          <span class="paw-prints">
            <Paw width="40" height="40" />
            <Paw width="40" height="40" />
            <Paw width="40" height="40" />
          </span>
        </h1>
        
        <p class="hero-description">
          Nossa equipe é especializada em bem-estar animal e está pronta para receber seu melhor amigo.
        </p>
        
        <div class="hero-buttons">
         <button class="header__cta" aria-label="Agendar atendimento" @click="handleContact('https://wa.me/554796180343')">
                    <WhatsAppIcon class="header__cta-icon" :size="20" />
                    <span class="header__cta-text">Agendar Atendimento</span>
                </button>
        </div>
        
        <div class="hero-features">
          <div class="feature-item">
            <CheckCircle class="feature-icon" :size="24" fillColor="#1F4D3F" />
            <span>Profissionais especializados</span>
          </div>
          <div class="feature-item">
            <CheckCircle class="feature-icon" :size="24" fillColor="#1F4D3F" />
            <span>Ambiente seguro e higienizado</span>
          </div>
          <div class="feature-item">
            <CheckCircle class="feature-icon" :size="24" fillColor="#1F4D3F" />
            <span>Produtos de alta qualidade</span>
          </div>
        </div>
      </div>
      
      <div class="hero-image">
        <img 
          src="https://images.unsplash.com/photo-1554456854-55a089fd4cb2?ixlib=rb-4.0.3&auto=format&fit=crop&w=1000&q=80" 
          alt="Cachorro sendo cuidado por profissional veterinário"
          class="hero-img"
        />
        <div class="image-overlay"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Paw from 'vue-material-design-icons/Paw.vue';
import WhatsAppIcon from 'vue-material-design-icons/Whatsapp.vue';
import CheckCircle from 'vue-material-design-icons/CheckCircle.vue';
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}


.header__cta {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.875rem 1.75rem;
    border-radius: 50px;
    border: 0;
    background-color: var(--color-primary);
    color: white;
    font-family: var(--font-sans);
    font-weight: 700;
    font-size: 0.95rem;
    cursor: pointer;
    transition: all 0.3s ease;
    white-space: nowrap;
    flex-shrink: 0;
}

.header__cta:hover {
    background-color: var(--color-accent);
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(31, 77, 63, 0.2);
}

.header__cta:active {
    transform: translateY(0);
}

.page-wrapper {
  min-height: 70vh;
  display: flex;
  align-items: center;
  justify-content: center;

}

.hero-banner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  width: 90%;
  margin: 0 auto;
  align-items: center;
}

.hero-content {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.hero-title {
  font-family: var(--font-display, sans-serif);
  font-size: 3.5rem;
  font-weight: 800;
  color: var(--color-primary, #1F4D3F);
  line-height: 1.1;
  margin-bottom: 10px;
}

.paw-prints {
  display: flex;
  gap: 10px;
  animation: float 3s ease-in-out infinite;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.hero-description {
  font-family: var(--font-sans, 'Plus Jakarta Sans', sans-serif);
  font-size: 1.4rem;
  color: #5a6a66;
}

.hero-buttons {
  display: flex;
  gap: 20px;
  margin-top: 10px;
  flex-wrap: wrap;
}

.cta-button {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  padding: 18px 36px;
  border-radius: 16px;
  font-family: var(--font-sans, 'Plus Jakarta Sans', sans-serif);
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border: none;
  min-width: 200px;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
}

.cta-whatsapp {
  background: linear-gradient(135deg, #25D366 0%, #128C7E 100%);
  color: white;
}

.cta-locations {
  background: linear-gradient(135deg, var(--color-primary, #1F4D3F) 0%, var(--color-accent, #8BA888) 100%);
  color: white;
}

.cta-button:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.15);
}

.cta-button:active {
  transform: translateY(-2px);
}

.button-icon {
  flex-shrink: 0;
}

.hero-features {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.feature-item {
  display: flex;
  align-items: center;
  gap: 12px;
}

.feature-icon {
  color: var(--color-primary, #1F4D3F);
  flex-shrink: 0;
}

.feature-item span {
  font-family: var(--font-sans, 'Plus Jakarta Sans', sans-serif);
  font-size: 1.1rem;
  color: #2d5550;
  font-weight: 500;
}

.hero-image {
  position: relative;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 25px 50px rgba(31, 77, 63, 0.2);
  height: 500px;
}

.hero-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  transition: transform 0.6s ease;
}

.hero-image:hover .hero-img {
  transform: scale(1.05);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(45deg, rgba(31, 77, 63, 0.1) 0%, transparent 100%);
  pointer-events: none;
}

/* Responsive */
@media (max-width: 1200px) {
  .hero-banner {
    gap: 40px;
  }
  
  .hero-title {
    font-size: 3rem;
  }
  
  .hero-description {
    font-size: 1.2rem;
  }
}

@media (max-width: 992px) {
  .hero-banner {
    grid-template-columns: 1fr;
    gap: 50px;
    text-align: center;
  }
  
  .hero-title {
    font-size: 2.8rem;
  }
  
  .paw-prints {
    justify-content: center;
  }
  
  .hero-description {
    max-width: 100%;
    margin: 0 auto;
  }
  
  .hero-buttons {
    justify-content: center;
  }
  
  .hero-features {
    align-items: center;
  }
  
  .hero-image {
    height: 400px;
    order: -1;
  }
}

@media (max-width: 768px) {
  .page-wrapper {
    min-height: 60vh;
    padding: 30px 0;
  }
  
  .hero-title {
    font-size: 2.3rem;
  }
  
  .hero-description {
    font-size: 1.1rem;
  }
  
  .cta-button {
    padding: 16px 28px;
    font-size: 1rem;
    min-width: 180px;
  }
  
  .hero-image {
    height: 350px;
  }
  
  .hero-buttons {
    flex-direction: column;
    align-items: center;
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 2rem;
  }
  
  .paw-prints {
    gap: 8px;
  }
  
  .hero-description {
    font-size: 1rem;
  }
  
  .cta-button {
    width: 100%;
    min-width: auto;
  }
  
  .hero-image {
    height: 300px;
  }
  
  .feature-item span {
    font-size: 1rem;
  }
}

/* Animações de entrada */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.hero-content {
  animation: fadeInUp 0.8s ease-out forwards;
}

.hero-image {
  animation: fadeInUp 0.8s ease-out 0.2s forwards;
  opacity: 0;
}
</style>