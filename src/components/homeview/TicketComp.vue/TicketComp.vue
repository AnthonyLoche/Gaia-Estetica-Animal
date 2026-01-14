<template>
  <div class="page-wrapper">
    <div class="promo-banner">
      <h2 class="title">
        Primeira vez na Gaia? 
        <span class="paw-prints">
            <Paw width="32" height="32" />
            <Paw width="32" height="32" />
            <Paw width="32" height="32" />
        </span>
      </h2>
      
      <p class="description">
        Ganhe <span class="highlight">15% de desconto</span> no primeiro banho e hidratação do seu pet.<br>
        Venha fazer parte da nossa família!
      </p>
      
      <button class="cta-button" @click="handleCoupon">
        Garantir meu cupom
      </button>
    </div>
  </div>
</template>

<script setup>
    import Paw from 'vue-material-design-icons/Paw.vue';
const handleCoupon = () => {
  alert('Cupom de 15% garantido! Entre em contato para agendar.');
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.page-wrapper {
  min-height: 40vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.promo-banner {
  background: linear-gradient(135deg, #2d5550 0%, #3d6b64 100%);
  border-radius: 24px;
  padding: 60px 40px;
  width: 90%;
  text-align: center;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);
}

.title {
  font-size: 3rem;
  font-weight: 700;
  color: white;
  margin-bottom: 24px;
  line-height: 1.2;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  flex-wrap: wrap;
}

.paw-prints {
  font-size: 32px;
  display: inline-block;
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-8px);
  }
}

.description {
  font-size: 16px;
  color: #e8f0ef;
  line-height: 1.6;
  margin-bottom: 32px;
}

.highlight {
  color: #ffd700;
  font-weight: 700;
  font-size: 18px;
}

.cta-button {
  background: white;
  color: #2d5550;
  border: none;
  border-radius: 12px;
  padding: 16px 40px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.cta-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
  background: #f8f8f8;
}

.cta-button:active {
  transform: translateY(0);
}

/* Responsive */
@media (max-width: 640px) {
  .promo-banner {
    padding: 40px 24px;
    border-radius: 16px;
  }
  
  .title {
    font-size: 28px;
  }
  
  .paw-prints {
    font-size: 26px;
  }
  
  .description {
    font-size: 14px;
  }
  
  .highlight {
    font-size: 16px;
  }
  
  .cta-button {
    padding: 14px 32px;
    font-size: 15px;
  }
}
</style>