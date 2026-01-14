<script setup>
import CalendarMonth from "vue-material-design-icons/CalendarMonth.vue";
import MenuIcon from "vue-material-design-icons/Menu.vue";
import CloseIcon from "vue-material-design-icons/Close.vue";
import { ref, onMounted, onUnmounted } from "vue";

const isMobileMenuOpen = ref(false);
const isScrolled = ref(false);

const toggleMobileMenu = () => {
    isMobileMenuOpen.value = !isMobileMenuOpen.value;
};

const closeMobileMenu = () => {
    isMobileMenuOpen.value = false;
};

const handleScroll = () => {
    isScrolled.value = window.scrollY > 10;
};

const handleWhatsapp = () => {
    window.open("https://wa.me/554796180343", "_blank");
};

onMounted(() => {
    window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
    window.removeEventListener("scroll", handleScroll);
});
</script>

<template>
    <header class="header" :class="{ 'header--scrolled': isScrolled }" role="banner">
        <div class="header__container">
            <router-link to="/" class="header__logo" @click="closeMobileMenu">
                <img src="../../assets/images/LogoGaia.png" alt="Gaia Estética Animal - Onde seu pet é família"
                    width="70" height="70" loading="lazy" />
                <span class="header__logo-text">Gaia Estética Animal</span>
            </router-link>

            <div class="header__desktop-content">
                <nav class="header__nav" aria-label="Navegação principal">
                    <ul class="header__nav-list">
                        <li class="header__nav-item">
                            <router-link to="/" class="header__nav-link" active-class="header__nav-link--active"
                                @click="closeMobileMenu">
                                Home
                            </router-link>
                        </li>
                        <li class="header__nav-item">
                            <router-link to="/services" class="header__nav-link" active-class="header__nav-link--active"
                                @click="closeMobileMenu">
                                Serviços
                            </router-link>
                        </li>
                        <li class="header__nav-item">
                            <router-link to="/about-us" class="header__nav-link" active-class="header__nav-link--active"
                                @click="closeMobileMenu">
                                Sobre Nós
                            </router-link>
                        </li>
                        <li class="header__nav-item">
                            <router-link to="/contact" class="header__nav-link" active-class="header__nav-link--active"
                                @click="closeMobileMenu">
                                Contato
                            </router-link>
                        </li>
                    </ul>
                </nav>

                <button class="header__cta" aria-label="Agendar atendimento" @click="handleWhatsapp()">
                    <CalendarMonth class="header__cta-icon" :size="20" />
                    <span class="header__cta-text">Agendar Atendimento</span>
                </button>
            </div>

            <button class="header__menu-toggle" @click="toggleMobileMenu" :aria-expanded="isMobileMenuOpen"
                aria-label="Abrir menu de navegação">
                <MenuIcon v-if="!isMobileMenuOpen" :size="28" />
                <CloseIcon v-else :size="28" />
            </button>
        </div>

        <transition name="slide">
            <nav v-if="isMobileMenuOpen" class="header__mobile-nav" aria-label="Navegação móvel">
                <div class="header__mobile-container">
                    <ul class="header__mobile-list">
                        <li class="header__mobile-item">
                            <router-link to="/" class="header__mobile-link" @click="closeMobileMenu">
                                Home
                            </router-link>
                        </li>
                        <li class="header__mobile-item">
                            <router-link to="/about" class="header__mobile-link" @click="closeMobileMenu">
                                Sobre
                            </router-link>
                        </li>
                        <li class="header__mobile-item">
                            <router-link to="/services" class="header__mobile-link" @click="closeMobileMenu">
                                Serviços
                            </router-link>
                        </li>
                        <li class="header__mobile-item">
                            <router-link to="/contact" class="header__mobile-link" @click="closeMobileMenu">
                                Contato
                            </router-link>
                        </li>
                    </ul>
                    <button class="header__mobile-cta" @click="closeMobileMenu">
                        <CalendarMonth class="header__mobile-cta-icon" :size="24" />
                        <span>Agendar Atendimento</span>
                    </button>
                </div>
            </nav>
        </transition>
    </header>
</template>

<style scoped>
.header {
    width: 100%;
    background-color: var(--color-background-light);
    padding: 1rem 0;
    box-shadow: 0 2px 10px rgba(31, 77, 63, 0.1);
    z-index: 1000;
    transition: all 0.3s ease;
}

.header--scrolled {
    padding: 0.75rem 0;
    box-shadow: 0 4px 12px rgba(31, 77, 63, 0.15);
}

.header__container {
    width: 90%;
    margin: 0 auto;
    padding: 0 1.5rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
}

.header__logo {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    text-decoration: none;
    color: var(--color-primary);
    font-family: var(--font-display);
    font-weight: 700;
    font-size: 1.25rem;
    transition: opacity 0.2s ease;
    flex-shrink: 0;
}

.header__logo:hover {
    opacity: 0.9;
}

.header__logo img {
    width: 70px;
    height: 70px;
    object-fit: contain;
    border-radius: 50%;
}

.header__logo-text {
    display: none;
}

@media (min-width: 768px) {
    .header__logo-text {
        display: inline;
    }
}

.header__desktop-content {
    display: none;
    align-items: center;
    gap: 3rem;
    flex: 1;
    justify-content: flex-end;
}

@media (min-width: 1024px) {
    .header__desktop-content {
        display: flex;
    }
}

.header__nav {
    display: flex;
    align-items: center;
}

.header__nav-list {
    display: flex;
    gap: 2rem;
    list-style: none;
    margin: 0;
    padding: 0;
}

.header__nav-item {
    position: relative;
}

.header__nav-link {
    text-decoration: none;
    color: var(--color-text);
    font-family: var(--font-sans);
    font-weight: 600;
    font-size: 1rem;
    padding: 0.5rem 0;
    transition: color 0.2s ease;
    position: relative;
    white-space: nowrap;
}

.header__nav-link:hover {
    color: var(--color-primary);
}

.header__nav-link--active {
    color: var(--color-primary);
}

.header__nav-link--active::after {
    content: '';
    position: absolute;
    bottom: -2px;
    left: 0;
    width: 100%;
    height: 2px;
    background-color: var(--color-primary);
    border-radius: 1px;
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

.header__cta-icon {
    flex-shrink: 0;
}

.header__menu-toggle {
    display: flex;
    align-items: center;
    justify-content: center;
    background: none;
    border: none;
    color: var(--color-primary);
    cursor: pointer;
    padding: 0.5rem;
    border-radius: 0.5rem;
    transition: background-color 0.2s ease;
    flex-shrink: 0;
}

.header__menu-toggle:hover {
    background-color: rgba(31, 77, 63, 0.1);
}

@media (min-width: 1024px) {
    .header__menu-toggle {
        display: none;
    }
}

.header__mobile-nav {
    top: 100%;
    left: 0;
    width: 100%;
    background-color: var(--color-background-light);
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    border-top: 1px solid rgba(31, 77, 63, 0.1);
}

.header__mobile-container {
    padding: 1.5rem;
    max-width: 1280px;
    margin: 0 auto;
}

.header__mobile-list {
    list-style: none;
    margin: 0 0 1.5rem 0;
    padding: 0;
}

.header__mobile-item {
    margin-bottom: 0.75rem;
}

.header__mobile-item:last-child {
    margin-bottom: 0;
}

.header__mobile-link {
    display: block;
    padding: 0.875rem 1rem;
    text-decoration: none;
    color: var(--color-text);
    font-family: var(--font-sans);
    font-weight: 600;
    font-size: 1.125rem;
    border-radius: 0.75rem;
    transition: all 0.2s ease;
}

.header__mobile-link:hover {
    background-color: rgba(31, 77, 63, 0.1);
    color: var(--color-primary);
}

.header__mobile-link.router-link-active {
    background-color: var(--color-primary);
    color: white;
}

.header__mobile-cta {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    width: 100%;
    padding: 1rem;
    border-radius: 0.75rem;
    border: 0;
    background-color: var(--color-primary);
    color: white;
    font-family: var(--font-sans);
    font-weight: 700;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.2s ease;
}

.header__mobile-cta:hover {
    background-color: var(--color-accent);
}

.header__mobile-cta-icon {
    flex-shrink: 0;
}

.slide-enter-active,
.slide-leave-active {
    transition: transform 0.3s ease, opacity 0.3s ease;
}

.slide-enter-from,
.slide-leave-to {
    transform: translateY(-10px);
    opacity: 0;
}

@media (max-width: 1023px) {
    .header__container {
        padding: 0 1rem;
    }
}

@media (min-width: 1024px) and (max-width: 1200px) {
    .header__desktop-content {
        gap: 2rem;
    }

    .header__nav-list {
        gap: 1.5rem;
    }
}
</style>