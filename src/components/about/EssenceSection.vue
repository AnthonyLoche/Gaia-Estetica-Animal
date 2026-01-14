<template>
    <section class="essence-section">
        <div class="container">
            <div class="essence-grid">
                <div class="image-wrapper">
                    <div class="image-glow"></div>
                    <img src="https://lh3.googleusercontent.com/aida-public/AB6AXuCtFRBiadrZM9pbQJVucuFHVDWljxlNkFyienh8f6BcUh7a8YtGJduXWCoQ5X6bQezXkg81HNXNKn4w64Cy3Sp5Vyv_w-t1qt4ApCXh2ynWqbxlpKK1ztinMDfpg5DAVwMflotbAVcrDKVr5VcWAJSJOcAZmDxs9maEEDe9-P53lLWL9NM4_x0PQdgMFS83zXuOvlV8HHYQS3iZW7EFMEIN5xrvmu7Li5ERq59gi1NfCBmu6XB0bzwVSIFoWR70VO7gOFQG38wqkw"
                        alt="Profissional cuidando de um cão" class="essence-img" />
                    <div class="quote-card">
                        <p>"Tratamos cada pet como se fosse parte da nossa própria família."</p>
                    </div>
                </div>

                <div class="essence-content">
                    <h2 class="section-title">
                        Nossa essência é o cuidado <div class="accent-text">humanizado</div>
                    </h2>

                    <div class="text-content">
                        <p>
                            A Gaia Estética Animal nasceu de um sonho compartilhado: transformar o momento do banho e
                            tosa em uma experiência de puro relaxamento e carinho para os pets.
                        </p>
                        <p>
                            Entendemos que, para muitos animais, a visita ao estética pode ser um momento de estresse.
                            Por isso, desenvolvemos métodos que respeitam o tempo, a personalidade e os limites de cada
                            cliente de quatro patas.
                        </p>
                        <p>
                            Nossa equipe é formada por profissionais apaixonados, que utilizam apenas produtos de alta
                            qualidade e técnicas modernas, garantindo não apenas a beleza, mas principalmente a saúde e
                            o bem-estar do seu pet.
                        </p>
                    </div>

                    <div class="tags-container">
                        <div class="tag">
                            <Heart class="tag-icon" :size="24" fillColor="#E8A8B1" />
                            <span>Dedicação Total</span>
                        </div>
                        <div class="tag">
                            <Medal class="tag-icon" :size="24" fillColor="#E8A8B1" />
                            <span>Profissionalismo</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import Heart from 'vue-material-design-icons/Heart.vue';
import Medal from 'vue-material-design-icons/Medal.vue';
</script>

<style scoped>
span {
    display: flex;
    align-items: center;
    justify-content: center;
}

.essence-section {
    padding: 5rem 0;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

.essence-grid {
    display: grid;
    gap: 4rem;
}

@media (min-width: 1024px) {
    .essence-grid {
        grid-template-columns: 1fr 1fr;
        align-items: center;
    }
}

.image-wrapper {
    position: relative;
    width: 100%;
}

.image-glow {
    position: absolute;
    inset: -1rem;
    background-color: rgba(232, 168, 177, 0.3);
    border-radius: 1.5rem;
    filter: blur(2rem);
    opacity: 0.4;
    transition: all 0.3s ease;
}

.image-wrapper:hover .image-glow {
    filter: blur(3rem);
}

.essence-img {
    position: relative;
    width: 100%;
    border-radius: 1.5rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    aspect-ratio: 4/5;
    object-fit: cover;
}

.quote-card {
    position: absolute;
    bottom: -1.5rem;
    right: -1.5rem;
    background-color: #fff;
    padding: 1.5rem;
    border-radius: 1.5rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    border: 1px solid rgba(232, 168, 177, 0.2);
    max-width: 20rem;
}

.dark .quote-card {
    background-color: var(--primary);
    color: var(--white);
}

.quote-card p {
    font-weight: 500;
    font-style: italic;
    font-size: 1.125rem;
    line-height: 1.4;
}

.essence-content {
    display: flex;
    flex-direction: column;
    gap: 2rem;
}

.section-title {
    font-family: 'Playfair Display', serif;
    font-size: 2.25rem;
    font-weight: 700;
    margin-bottom: 1rem;
    color: var(--primary);
}

.dark .section-title {
    color: var(--white);
}

.accent-text {
    color: #E8A8B1;
    font-style: italic;
    font-family: var(--font-display), serif;
}

.text-content {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
}

.text-content p {
    font-size: 1.125rem;
    color: rgba(25, 64, 49, 0.8);
    line-height: 1.75;
}

.dark .text-content p {
    color: rgba(242, 235, 196, 0.8);
}

.tags-container {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    padding-top: 1rem;
}

.tag {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    background-color: rgba(255, 255, 255, 0.5);
    padding: 0.75rem 1.5rem;
    border-radius: 9999px;
    font-weight: 700;
}

.dark .tag {
    background-color: rgba(255, 255, 255, 0.05);
}

.tag-icon {
    flex-shrink: 0;
}

/* Responsividade */
@media (max-width: 768px) {
    .essence-section {
        padding: 3rem 0;
    }

    .section-title {
        font-size: 1.875rem;
    }

    .text-content p {
        font-size: 1rem;
    }

    .quote-card {
        position: relative;
        bottom: 0;
        right: 0;
        margin-top: 1.5rem;
        max-width: 100%;
    }
}

@media (max-width: 640px) {
    .essence-grid {
        gap: 2.5rem;
    }

    .section-title {
        font-size: 1.5rem;
    }

    .tag {
        padding: 0.5rem 1rem;
        font-size: 0.875rem;
    }

    .tag-icon {
        width: 20px;
        height: 20px;
    }
}
</style>