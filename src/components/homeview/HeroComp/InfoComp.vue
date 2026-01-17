<script setup>
import PawIcon from "vue-material-design-icons/Paw.vue";
import WhatsAppIcon from "vue-material-design-icons/Whatsapp.vue";
import DogService from "vue-material-design-icons/DogService.vue";
import CreditCardOutline from "vue-material-design-icons/CreditCardOutline.vue";
import router from "@/router";

const handleContact = (url) => {
    window.open(url, "_blank");
};

const packageInfo = {
    title: '❗Pacote Mensal e Quinzenal❗',
    description: 'Serviços regulares com agendamento fixo e preço especial para cuidados mensais.',
    linkText: 'CONSULTAR PACOTE',
    variant: 'dark-green',
    icon: CreditCardOutline,
    whatsappMessage: 'Oi! Gostaria de consultar os valores dos pacotes mensais e quinzenais'
};

const handlePackageContact = () => {
    const message = encodeURIComponent(packageInfo.whatsappMessage);
    window.open(`https://wa.me/554796180343?text=${message}`, "_blank");
};
</script>

<template>
    <article class="info-gero">
        <div class="text">
            <div class="tag">
                <PawIcon :size="24" />
                Especialistas em Bem-Estar
            </div>
            <div>
                <h1 class="title">
                    <div>Gaia Estética</div>
                    <div>Animal - Onde </div>
                    <div class="align">seu pet é <div class="marked">família</div>
                    </div>
                </h1>
            </div>
        </div>
        <div class="desc">
            <div class="subtitle">Proporcionamos um atendimento humanizado e carinhoso cuidando da estética e saúde do
                seu melhor amigo com os melhores produtos do mercado</div>
            <div class="buttons">
                <button class="header__cta" aria-label="Agendar atendimento" @click="handleContact('https://wa.me/554796180343')">
                    <WhatsAppIcon class="header__cta-icon" :size="20" />
                    <span class="header__cta-text">Agendar Atendimento</span>
                </button>
                <button class="header__blank-cta" aria-label="Conhecer serviços" @click="router.push('/services')">
                    <DogService class="header__cta-icon" :size="20" />
                    <span class="header__cta-text">Conhecer Serviços</span>
                </button>
            </div>
            
            <div class="package-card" @click="handlePackageContact">
                <div class="package-icon">
                    <component :is="packageInfo.icon" :size="32" />
                </div>
                <div class="package-content">
                    <h3 class="package-title">{{ packageInfo.title }}</h3>
                    <p class="package-description">{{ packageInfo.description }}</p>
                    <button class="package-button" :class="packageInfo.variant">
                        <span class="package-button-text">{{ packageInfo.linkText }}</span>
                        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                            <path d="M5 12h14M12 5l7 7-7 7"/>
                        </svg>
                    </button>
                </div>
            </div>
            
            <div class="plus">
                <div>
                    <img src="https://images.pexels.com/photos/128817/pexels-photo-128817.jpeg" alt="" class="circle">
                    <img src="https://images.pexels.com/photos/220938/pexels-photo-220938.jpeg" alt="" class="circle">
                    <img src="https://images.pexels.com/photos/406014/pexels-photo-406014.jpeg" alt="" class="circle">
                </div>
                <p style="margin-left: 1rem;">+Mais de <strong>500 pets</strong> atendidos</p>
            </div>
        </div>
    </article>
</template>

<style scoped>
span {
    display: flex;
    align-items: center;
    justify-content: center;
}

.align{
    display: flex; gap: 0.75rem;
}

img.circle {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background-color: var(--color-accent);  
    margin-right: -10px;
    border: 2px solid white;
}

.plus {
    display: flex;
    align-items: center;
    margin-top: 1.5rem;
}

.tag {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    width: fit-content;
    font-weight: 600;
    padding: .5rem;
    color: var(--color-primary);
    border-radius: 50px;
    background-color: var(--color-secondary-20);
}

.title {
    color: var(--color-primary);
    font-size: 5rem;
    font-weight: 700;
    line-height: 1.3;
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

/* BOTÃO "CONHECER SERVIÇOS" COM ANIMAÇÕES AVANÇADAS */
.header__blank-cta {
    display: flex;
    align-items: center;
    gap: 0.6rem;
    padding: 0.9rem 2rem;
    border-radius: 999px;
    border: none;
    
    /* Gradiente animado */
    background: linear-gradient(
        135deg,
        #FF6B9D 0%,
        #FF4081 25%,
        #E91E63 50%,
        #C2185B 100%
    );
    background-size: 400% 400%;
    
    color: #ffffff;
    font-family: var(--font-sans);
    font-weight: 800;
    font-size: 1rem;
    letter-spacing: 0.4px;
    cursor: pointer;
    white-space: nowrap;
    flex-shrink: 0;
    
    position: relative;
    overflow: hidden;
    z-index: 1;
    transition: 0.2s ease-in-out;    
    animation: gradientMove 8s ease infinite, borderGlow 3s ease-in-out infinite alternate;
}

@keyframes gradientMove {
    0%, 100% {
        background-position: 0% 50%;
    }
    50% {
        background-position: 100% 50%;
    }
}

/* Brilho na borda */
@keyframes borderGlow {
    0% {
        box-shadow: 
            0 0 10px rgba(255, 107, 157, 0.4),
            0 0 20px rgba(255, 64, 129, 0.3),
            0 0 30px rgba(233, 30, 99, 0.2),
            inset 0 0 15px rgba(255, 255, 255, 0.1);
    }
    100% {
        box-shadow: 
            0 0 15px rgba(255, 107, 157, 0.6),
            0 0 25px rgba(255, 64, 129, 0.5),
            0 0 35px rgba(233, 30, 99, 0.3),
            inset 0 0 20px rgba(255, 255, 255, 0.2);
    }
}

/* Efeito de corrente/partículas na borda */
.header__blank-cta::before {
    content: '';
    position: absolute;
    top: -2px;
    left: -2px;
    right: -2px;
    bottom: -2px;
    border-radius: 999px;
    background: linear-gradient(
        45deg,
        #FF6B9D,
        #FF4081,
        #E91E63,
        #C2185B,
        #FF6B9D
    );
    background-size: 400% 400%;
    z-index: -1;
    animation: borderFlow 4s linear infinite;
    filter: blur(3px);
    opacity: 0.8;
}

@keyframes borderFlow {
    0% {
        background-position: 0% 50%;
        transform: rotate(0deg);
    }
    50% {
        background-position: 100% 50%;
    }
    100% {
        background-position: 0% 50%;
        transform: rotate(360deg);
    }
}

/* Efeito de brilho deslizante */
.header__blank-cta::after {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(
        90deg,
        transparent,
        rgba(255, 255, 255, 0.3),
        transparent
    );
    transition: left 0.7s ease;
    z-index: 0;
}

.header__blank-cta:hover::after {
    left: 100%;
}

/* Conteúdo do botão acima dos efeitos */
.header__blank-cta > * {
    position: relative;
    z-index: 2;
}

.header__blank-cta:hover {
    transform: translateY(-3px) scale(1.03);
    animation: gradientMove 4s ease infinite, borderGlow 1.5s ease-in-out infinite alternate;
}

.header__blank-cta:active {
    transform: translateY(0) scale(1);
    animation-play-state: paused;
}

.buttons {
    display: flex;
    gap: 1rem;
    margin-top: 1.5rem;
}

.marked {
    color: var(--color-secondary);
    text-decoration: underline;
    text-decoration-thickness: 4px;
    text-underline-offset: 8px;
    font-weight: 700;
    font-style: italic;
}

.subtitle {
    color: #555555;
    font-size: 1.25rem;
    width: 80%;
    margin-bottom: 1.5rem;
}

/* ESTILOS PARA O CARD DO PACOTE */
.package-card {
    margin-top: 2rem;
    padding: 1.5rem;
    background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
    border-radius: 16px;
    border: 2px solid #e0e0e0;
    display: flex;
    gap: 1.25rem;
    align-items: flex-start;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}

.package-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1);
    border-color: var(--color-primary);
    background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
}

.package-icon {
    background: var(--color-primary);
    color: white;
    padding: 0.75rem;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.package-content {
    flex: 1;
}

.package-title {
    color: var(--color-primary);
    font-size: 1.25rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
}

.package-description {
    color: #666;
    font-size: 0.95rem;
    line-height: 1.4;
    margin-bottom: 1rem;
}

.package-button {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.75rem 1.5rem;
    border-radius: 50px;
    border: none;
    background: var(--color-primary);
    color: white;
    font-family: var(--font-sans);
    font-weight: 700;
    font-size: 0.9rem;
    cursor: pointer;
    transition: all 0.3s ease;
}

.package-button.dark-green {
    background: #2e7d32;
}

.package-button.dark-green:hover {
    background: #1b5e20;
    transform: translateX(4px);
}

.package-button-text {
    display: inline-block;
}

@media screen and (max-width:1024px) {
    .title{
        font-size: 3rem;
        word-spacing: 10px;
    }

    .buttons {
        flex-direction: column;
        align-items: flex-start;
    }

    .subtitle {
        width: 100%;
    }

    button{
        width: 100%;
        align-items: center;
        justify-content: center;
    }

    .align{
        display: grid;
    }

    .marked{
        margin-top: -12px;
    }

    .text{
        display: flex;
        gap: 1rem;
        flex-direction: column;
        margin-bottom: 1rem;
        text-align: center;
        align-items: center;
    }
    
    .package-card {
        flex-direction: column;
        align-items: center;
        text-align: center;
        padding: 1.25rem;
    }
    
    .package-icon {
        margin-bottom: 0.75rem;
    }
    
    /* Ajustes para mobile */
    .header__blank-cta {
        animation: gradientMove 12s ease infinite, borderGlow 4s ease-in-out infinite alternate;
    }
}
</style>