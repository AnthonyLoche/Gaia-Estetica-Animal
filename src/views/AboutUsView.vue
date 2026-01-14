<template>
    <div class="page-container">
        <HeaderMain />

        <main class="main-content">
            <section class="section-animate" data-animate="hero">
                <HeroAbout />
            </section>

            <section class="section-animate" data-animate="fade-up">
                <EssenceSection />
            </section>

            <section class="section-animate" data-animate="zoom-in">
                <QuoteSection />
            </section>

            <section class="section-animate delay-child" data-animate="fade-up">
                <FeaturesSection />
            </section>

            <section class="section-animate" data-animate="slide-left">
                <GallerySection />
            </section>
        </main>

        <FooterMain />
    </div>
</template>

<script setup>
import { onMounted, onUnmounted } from 'vue'
import {
    HeaderMain,
    FooterMain,
    HeroAbout,
    EssenceSection,
    QuoteSection,
    FeaturesSection,
    GallerySection
} from '@/components'

const initIntersectionObservers = () => {
    const observer = new IntersectionObserver(
        entries => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('animate-in')

                    if (entry.target.classList.contains('delay-child')) {
                        const children = entry.target.querySelectorAll('[data-delay]')
                        children.forEach((el, index) => {
                            const delay = el.dataset.delay || index * 100
                            setTimeout(() => el.classList.add('animate-in'), delay)
                        })
                    }
                }
            })
        },
        { threshold: 0.1 }
    )

    document
        .querySelectorAll('[data-animate], section, .section')
        .forEach(el => observer.observe(el))

    return observer
}

onMounted(() => {
    const observer = initIntersectionObservers()
    onUnmounted(() => observer.disconnect())
})
</script>

<style scoped>
</style>