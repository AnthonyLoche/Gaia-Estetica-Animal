<script setup>
import CheckCircleOutline from 'vue-material-design-icons/CheckCircleOutline.vue';
import { computed } from 'vue';

const props = defineProps({
    image: {
        type: String,
        required: true
    },
    title: {
        type: String,
        required: true
    },
    description: {
        type: String,
        required: true
    },
    features: {
        type: Array,
        required: true,
        validator: (value) => Array.isArray(value) && value.length > 0
    }
});

// Computed para garantir que features seja um array
const safeFeatures = computed(() => {
    return Array.isArray(props.features) ? props.features : [];
});
</script>

<template>
    <article class="service-card">
        <!-- Imagem do serviço -->
        <div class="service-card__image-container">
            <img :src="image" :alt="`Imagem do serviço: ${title}`" class="service-card__image" loading="lazy" />
            <div class="service-card__image-overlay"></div>
        </div>

        <!-- Conteúdo do card -->
        <div class="service-card__content">
            <div class="service-card__header">
                <h3 class="service-card__title">{{ title }}</h3>
                <div class="service-card__description">{{ description }}</div>
            </div>

            <!-- Lista de características -->
            <ul class="service-card__features">
                <li v-for="(feature, index) in safeFeatures" :key="index" class="service-card__feature-item">
                    <CheckCircleOutline class="service-card__feature-icon" :size="20" fillColor="#1F4D3F" />
                    <span class="service-card__feature-text">{{ feature }}</span>
                </li>
            </ul>
        </div>
    </article>
</template>

<style scoped>
.service-card {
    width: 100%;
    display: flex;
    flex-direction: column;
    background-color: white;
    border-radius: var(--radius-2xl);
    overflow: hidden;
    box-shadow: 0 10px 30px rgba(31, 77, 63, 0.1);
    transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    border: 1px solid rgba(244, 167, 185, 0.1);
    position: relative;
    padding: 1rem;
}

.service-card:hover {
    transform: translateY(-10px);
    box-shadow:
        0 20px 40px rgba(31, 77, 63, 0.15),
        0 0 0 1px rgba(244, 167, 185, 0.2);
}

.service-card__image-container {
    position: relative;
    width: 100%;
    height: 220px;
    overflow: hidden;
    border-radius: var(--radius-default);

}

.service-card__image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.6s ease;
    border-radius: var(--radius-default);
}

.service-card:hover .service-card__image {
    transform: scale(1.05);
}

.service-card__image-overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 50%;
    background: linear-gradient(to top, rgba(31, 77, 63, 0.3), transparent);
}

.service-card__content {
    padding: 1.75rem;
    display: flex;
    flex-direction: column;
    flex: 1;
    gap: 1.25rem;
}

.service-card__header {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
}

.service-card__title {
    font-family: var(--font-display);
    font-size: 1.5rem;
    font-weight: 700;
    color: var(--color-primary);
    line-height: 1.2;
    margin: 0;
}

.service-card__description {
    font-family: var(--font-sans);
    font-size: 0.95rem;
    line-height: 1.5;
    color: #555555;
    margin: 0;
}

.service-card__features {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
}

.service-card__feature-item {
    display: flex;
    align-items: flex-start;
    gap: 0.75rem;
}

.service-card__feature-icon {
    flex-shrink: 0;
    color: var(--color-primary);
    margin-top: 0.125rem;
}

.service-card__feature-text {
    font-family: var(--font-sans);
    font-size: 0.95rem;
    line-height: 1.4;
    color: #333333;
    flex: 1;
}

.service-card__button {
    margin-top: auto;
    padding: 1rem 1.5rem;
    background-color: var(--color-primary);
    color: white;
    border: none;
    border-radius: var(--radius-default);
    font-family: var(--font-sans);
    font-weight: 600;
    font-size: 1rem;
    cursor: pointer;
    transition: all 0.3s ease;
    text-align: center;
    width: 100%;
}

.service-card__button:hover {
    background-color: var(--color-accent);
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(31, 77, 63, 0.2);
}

.service-card__button:active {
    transform: translateY(0);
}

@media (max-width: 768px) {
    .service-card {
        max-width: 100%;
    }

    .service-card__content {
        padding: 1.5rem;
    }

    .service-card__title {
        font-size: 1.35rem;
    }
}
</style>