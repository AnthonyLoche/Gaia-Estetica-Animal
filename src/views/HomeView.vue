<script setup>
import { HeaderMain, HeroMain, StacksSection, FooterMain, ServicesMain, TicketComp, LocationComp } from '@/components';
import { onMounted, onUnmounted } from 'vue';

const initIntersectionObservers = () => {
  const observer = new IntersectionObserver(entries => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('animate-in');

        if (entry.target.classList.contains('delay-child')) {
          const children = entry.target.querySelectorAll('[data-delay]');
          children.forEach((el, index) => {
            const delay = el.dataset.delay || index * 100;
            setTimeout(() => el.classList.add('animate-in'), delay);
          });
        }
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('[data-animate], section, .section')
    .forEach(el => observer.observe(el));

  return observer;
};

onMounted(() => {
  const observer = initIntersectionObservers();
  onUnmounted(() => observer.disconnect());
});
</script>

<template>
  <div class="page-container">
    <HeaderMain />

    <main class="main-content">
      <section class="section-animate" data-animate="hero">
        <HeroMain />
      </section>

      <section class="section-animate delay-child" data-animate="fade-up">
        <StacksSection />
      </section>

      <section class="section-animate delay-child" data-animate="fade-up">
        <ServicesMain />
      </section>

      <section class="section-animate" data-animate="slide-left">
        <TicketComp />
      </section>

      <section class="section-animate" data-animate="zoom-in">
        <LocationComp />
      </section>
    </main>

    <FooterMain />
  </div>
</template>
