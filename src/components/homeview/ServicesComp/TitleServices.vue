<script setup>
</script>

<template>
    <article>
        <h2>Serviços que encantam</h2>
        <p>Oferecemos o cuidado completo que seu pet merece para brilhar por onde passar.</p>
    </article>
</template>

<style scoped>
    article {
        text-align: center;
    }

    h2 {
        font-size: 3rem;
        margin-bottom: 0.5rem;
        color: var(--color-primary);
    }

    p {
        font-size: 1.2rem;
        color: var(--color-text-secondary);
    }

    @media screen and (max-width: 1024px) {
        h2 {
            font-size: 2.5rem;
        }

        p {
            font-size: 1rem;
        }
    }
</style>