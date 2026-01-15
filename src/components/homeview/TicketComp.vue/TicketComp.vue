<template>
  <div class="page-wrapper">
    <section class="experience-banner">
      
      <span class="badge">
        <Paw width="18" height="18" />
        Cuidado premium
      </span>

      <h2 class="title">
        Um novo jeito de cuidar<br />
        <span>de quem você ama</span>
      </h2>

      <p class="description">
        Na <strong>Gaia</strong>, cada banho é um momento de calma,
        carinho e bem-estar.<br />
        Seu pet merece mais do que um serviço — merece uma experiência.
      </p>

      <div class="actions">
        <button class="primary" @click="handleContact('https://wa.me/554796180343')">
          Agendar um horário
        </button>

      </div>

    </section>
  </div>
</template>

<script setup>
import Paw from 'vue-material-design-icons/Paw.vue'

const handleContact = (url) => {
    window.open(url, "_blank");
};
</script>

<style scoped>
/* ===============================
   RESET
================================ */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* ===============================
   WRAPPER
================================ */
.page-wrapper {
  min-height: 45vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40px 0;
}

/* ===============================
   BANNER
================================ */
.experience-banner {
  background: linear-gradient(135deg, #1f3d38 0%, #2d5550 100%);
  border-radius: 28px;
  padding: 64px 48px;
  width: 90%;
  text-align: center;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.2);
  color: white;
}

/* ===============================
   BADGE
================================ */
.badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: rgba(255, 255, 255, 0.15);
  padding: 8px 16px;
  border-radius: 999px;
  font-size: 14px;
  margin-bottom: 24px;
}

/* ===============================
   TITLE
================================ */
.title {
  font-size: 3rem;
  font-weight: 700;
  line-height: 1.15;
  margin-bottom: 24px;
}

.title span {
  color: #a8e6cf;
}

/* ===============================
   TEXT
================================ */
.description {
  font-size: 17px;
  line-height: 1.7;
  color: #e6f2ef;
  margin-bottom: 40px;
}

/* ===============================
   ACTIONS
================================ */
.actions {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}

button {
  border: none;
  border-radius: 14px;
  padding: 16px 36px;
  font-size: 15px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

/* Primary */
.primary {
  background: white;
  color: #2d5550;
}

.primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

/* Secondary */
.secondary {
  background: transparent;
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.5);
}

.secondary:hover {
  background: rgba(255, 255, 255, 0.1);
}

/* ===============================
   RESPONSIVE
================================ */
@media (max-width: 768px) {
  .experience-banner {
    padding: 48px 28px;
    border-radius: 20px;
  }

  .title {
    font-size: 2.2rem;
  }

  .description {
    font-size: 15px;
  }
}

@media (max-width: 480px) {
  .title {
    font-size: 1.9rem;
  }

  button {
    width: 100%;
  }
}
</style>
