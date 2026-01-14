<template>
    <section class="features-section">
        <div class="container">
            <div class="section-header">
                <h3 class="section-title">Por que escolher a Gaia?</h3>
                <p class="section-subtitle">Os diferenciais que fazem o rabo abanar de alegria.</p>
            </div>

            <div class="features-grid">
                <div class="feature-card">
                    <div class="feature-icon">
                        <Paw class="feature-icon-svg" :size="32" fillColor="#194031" />
                    </div>
                    <h4>Cuidado Gentil</h4>
                    <p>Técnicas de manejo que priorizam a calma e o conforto do animal durante todo o processo.</p>
                </div>

                <div class="feature-card">
                    <div class="feature-icon">
                        <HandWash class="feature-icon-svg" :size="32" fillColor="#194031" />
                    </div>
                    <h4>Produtos Premium</h4>
                    <p>Utilizamos linhas dermatológicas de ponta, seguras e com fragrâncias suaves e hipoalergênicas.
                    </p>
                </div>

                <div class="feature-card">
                    <div class="feature-icon">
                        <Eye class="feature-icon-svg" :size="32" fillColor="#194031" />
                    </div>
                    <h4>Transparência</h4>
                    <p>Espaço aberto e visível. Você pode acompanhar o cuidado que seu pet está recebendo.</p>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import Paw from 'vue-material-design-icons/Paw.vue';
import HandWash from 'vue-material-design-icons/HandWash.vue';
import Eye from 'vue-material-design-icons/Eye.vue';
</script>

<style scoped>
.features-section {
    padding: 6rem 0;
    background-color: rgba(255, 255, 255, 0.3);
}

.dark .features-section {
    background-color: rgba(255, 255, 255, 0.05);
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

.section-header {
    text-align: center;
    margin-bottom: 4rem;
}

.section-title {
    font-family: var(--font-display, 'Playfair Display'), serif;
    font-size: 2.25rem;
    font-weight: 700;
    margin-bottom: 1rem;
    color: #194031;
}

.dark .section-title {
    color: #F2EBC4;
}

.section-subtitle {
    color: rgba(25, 64, 49, 0.8);
    font-size: 1.125rem;
}

.dark .section-subtitle {
    color: rgba(242, 235, 196, 0.8);
}

.features-grid {
    display: grid;
    gap: 2rem;
}

@media (min-width: 768px) {
    .features-grid {
        grid-template-columns: repeat(3, 1fr);
    }
}

.feature-card {
    background-color: #F2EBC4;
    padding: 2.5rem;
    border-radius: 1.5rem;
    border: 1px solid rgba(25, 64, 49, 0.05);
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    transition: all 0.3s ease;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.dark .feature-card {
    background-color: #0D1F18;
}

.feature-card:hover {
    transform: translateY(-0.5rem);
}

.feature-icon {
    width: 4rem;
    height: 4rem;
    background-color: rgba(232, 168, 177, 0.2);
    border-radius: 1.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 1.5rem;
    transition: all 0.3s ease;
}

.feature-card:hover .feature-icon {
    transform: scale(1.1);
    background-color: rgba(232, 168, 177, 0.3);
}

.feature-icon-svg {
    transition: transform 0.3s ease;
}

.feature-card:hover .feature-icon-svg {
    transform: scale(1.1);
}

.dark .feature-icon-svg {
    fill: #F2EBC4;
}

.feature-card h4 {
    font-size: 1.25rem;
    font-weight: 700;
    margin-bottom: 1rem;
    color: #194031;
    font-family: var(--font-display, 'Playfair Display'), serif;
}

.dark .feature-card h4 {
    color: #F2EBC4;
}

.feature-card p {
    color: rgba(25, 64, 49, 0.8);
    line-height: 1.6;
    font-size: 0.95rem;
}

.dark .feature-card p {
    color: rgba(242, 235, 196, 0.8);
}

/* Alternativa: Se quiser manter a cor do ícone no dark mode */
:deep(.feature-icon-svg) {
    fill: #194031;
}

.dark :deep(.feature-icon-svg) {
    fill: #F2EBC4;
}

/* Responsividade */
@media (max-width: 768px) {
    .features-section {
        padding: 4rem 0;
    }

    .section-title {
        font-size: 1.875rem;
    }

    .feature-card {
        padding: 2rem;
    }
    
    .feature-icon {
        width: 3.5rem;
        height: 3.5rem;
    }
    
    .feature-icon-svg {
        width: 28px;
        height: 28px;
    }
}

@media (max-width: 640px) {
    .features-section {
        padding: 3rem 0;
    }

    .features-grid {
        grid-template-columns: 1fr;
    }

    .section-title {
        font-size: 1.5rem;
    }
    
    .feature-card {
        padding: 1.75rem;
    }
}
</style>