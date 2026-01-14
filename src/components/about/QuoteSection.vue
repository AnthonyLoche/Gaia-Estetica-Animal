<template>
    <section class="quote-section">
        <div class="container">
            <span class="quote-icon material-symbols-rounded">
                <FormatQuoteClose size="50" />
            </span>
            <h2 class="quote-text">
                "Atendimento com carinho e profissionalismo é o pilar que sustenta cada procedimento na Gaia."
            </h2>
            <div class="divider"></div>
        </div>
    </section>
</template>

<script setup>
import FormatQuoteClose from 'vue-material-design-icons/FormatQuoteClose.vue';
</script>

<style scoped>
.quote-section {
    background-color: #194031;
    padding: 6rem 0;
    text-align: center;
}

.dark .quote-section {
    background-color: #194031;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

.quote-icon {
    color: #E8A8B1;
    margin-bottom: 2rem;
}

.quote-text {
    font-family: var(--font-display), serif;
    font-size: 1.875rem;
    font-style: italic;
    color: #F2EBC4;
    max-width: 64rem;
    margin: 0 auto;
    line-height: 1.3;
}

.dark .quote-text {
    color: #F2EBC4;
}

@media (min-width: 768px) {
    .quote-text {
        font-size: 3rem;
    }
}

.divider {
    width: 5rem;
    height: 0.25rem;
    background-color: #E8A8B1;
    border-radius: 0.125rem;
    margin: 2.5rem auto 0;
}

/* Responsividade */
@media (max-width: 768px) {
    .quote-section {
        padding: 4rem 0;
    }

    .quote-icon {
        font-size: 3rem;
        margin-bottom: 1.5rem;
    }

    .quote-text {
        font-size: 1.5rem;
        padding: 0 1rem;
    }

    .divider {
        margin-top: 2rem;
    }
}

@media (max-width: 640px) {
    .quote-section {
        padding: 3rem 0;
    }

    .quote-text {
        font-size: 1.25rem;
    }
}
</style>