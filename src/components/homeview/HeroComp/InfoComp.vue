<script setup>
import PawIcon from "vue-material-design-icons/Paw.vue";
import WhatsAppIcon from "vue-material-design-icons/Whatsapp.vue";
import DogService from "vue-material-design-icons/DogService.vue";

const handleContact = (url) => {
    window.open(url, "_blank");
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
                    <div style="display: flex; gap: 0.75rem;">seu pet é <div class="marked">família</div>
                    </div>
                </h1>
            </div>
        </div>
        <div class="desc">
            <div class="subtitle">Proporcionamos um atendimento humanizado e carinhoso cuidadndo da estética e saúde do
                seu melhor amigo com os melhores produtos do mercado</div>
            <div class="buttons">
                <button class="header__cta" aria-label="Agendar atendimento" @click="handleContact('https://wa.me/554796180343')">
                    <WhatsAppIcon class="header__cta-icon" :size="20" />
                    <span class="header__cta-text">Agendar Atendimento</span>
                </button>
                <button class="header__blank-cta" aria-label="Agendar atendimento">
                    <DogService class="header__cta-icon" :size="20" />
                    <span class="header__cta-text">Conhecer Serviços</span>
                </button>
            </div>
            <div class="plus">
                <div>
                    
                <img src="https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/dog-puppy-on-garden-royalty-free-image-1586966191.jpg?crop=1.00xw:0.669xh;0,0.190xh&resize=1200:*" alt="" class="circle">
                <img src="https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/dog-puppy-on-garden-royalty-free-image-1586966191.jpg?crop=1.00xw:0.669xh;0,0.190xh&resize=1200:*" alt="" class="circle">
                <img src="https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/dog-puppy-on-garden-royalty-free-image-1586966191.jpg?crop=1.00xw:0.669xh;0,0.190xh&resize=1200:*" alt="" class="circle">
                
                </div>
                <p style="margin-left: 1rem;">+Mais de <strong>500 pets</strong> felizes atendidos</p>
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

img.circle {
    width: 40px;
    height: 40px;
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

.buttons {
    display: flex;
    gap: 1rem;
    margin-top: 1.5rem;
}


.header__blank-cta {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.875rem 1.75rem;
    border-radius: 50px;
    border: 0;
    background-color: #c1c1c1;
    color: white;
    font-family: var(--font-sans);
    font-weight: 700;
    font-size: 0.95rem;
    cursor: pointer;
    transition: all 0.3s ease;
    white-space: nowrap;
    flex-shrink: 0;
}

.header__blank-cta:hover {
    background-color: #8a8585;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(31, 77, 63, 0.2);
}

.header__blank-cta:active {
    transform: translateY(0);
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
}
</style>