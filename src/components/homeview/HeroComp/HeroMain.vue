<script setup>
import InfoComp from './InfoComp.vue';
import PhotoComp from './PhotoComp.vue';
</script>

<template>
    <section class="hero-main">
        <div class="container-main">
            <div class="one">
                <InfoComp />
            </div>
            <PhotoComp />
        </div>
    </section>
</template>

<style scoped>
.hero-main {
    width: 100%;
    height: 80vh;
    font-family: var(--font-display);
    margin-top: 2rem;
}

.container-main {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    width: 90%;
    height: 100%;
    margin: 0 auto;
}

.one{
    display: flex;
    flex-direction: column;
    justify-content: center;
}
</style>