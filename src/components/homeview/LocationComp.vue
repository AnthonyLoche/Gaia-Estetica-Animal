<template>
    <div class="page-wrapper">
        <section class="location-section">
            <div class="info-container">
                <h2 class="section-title">Onde nos encontrar</h2>

                <div class="info-item">
                    <div class="icon-wrapper">
                        <MapMarker width="20" height="20" />
                    </div>
                    <div class="info-content">
                        <h3 class="info-title">Nosso Endereço</h3>
                        <p class="info-text">Rua dos Cravos, 181 - Bairro Guanabara</p>
                        <p class="info-text">Joinville, SC</p>
                    </div>
                </div>

                <div class="info-item">
                    <div class="icon-wrapper">
                        <Clock width="20" height="20" />
                    </div>
                    <div class="info-content">
                        <h3 class="info-title">Horário de Funcionamento</h3>
                        <p class="info-text">Segunda a Sexta: 08:00 às 18:00</p>
                        <p class="info-text">Sábado: 08:00 às 13:00</p>
                    </div>
                </div>

                <div class="info-item">
                    <div class="icon-wrapper">
                        <Phone width="20" height="20" />
                    </div>
                    <div class="info-content">
                        <h3 class="info-title">Contato</h3>
                        <p class="info-text">+55 47 9618-0343</p>
                        <p class="info-text">gaiaesteticaanimal@gmail.com</p>
                    </div>
                </div>

                <div class="social-links">
                    <a href="https://www.instagram.com/gaiaesteticaanimal/" class="social-icon" aria-label="Instagram" target="blank">
                        <Instagram width="20" height="20" />
                    </a>
                    <a href="https://wa.me/554796180343" class="social-icon" aria-label="Facebook" target="blank">
                        <Phone width="20" height="20" />
                    </a>
                </div>
            </div>

            <div class="map-container">
                <iframe
                    src="https://www.google.com/maps?q=R.%20dos%20Cravos,%20181%20-%20Guanabara,%20Joinville%20-%20SC,%2089207-740&output=embed"
                    width="100%" height="100%" style="border:0;" allowfullscreen loading="lazy"
                    referrerpolicy="no-referrer-when-downgrade">
                </iframe>
            </div>

        </section>
    </div>
</template>

<script setup>
import Phone from "vue-material-design-icons/Phone.vue";
import Instagram from "vue-material-design-icons/Instagram.vue";
import Clock from "vue-material-design-icons/Clock.vue";
import MapMarker from "vue-material-design-icons/MapMarker.vue";
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.page-wrapper {
    min-height: 50vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 40px 0;
}

span {
    display: flex;
    align-items: center;
    justify-content: center;
}

.location-section {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 40px;
    width: 90%;
    margin: auto;
}

.info-container {
    padding: 50px 40px;
    border-radius: 16px;
}

.section-title {
    font-size: 32px;
    font-weight: 700;
    color: #2d5550;
    margin-bottom: 40px;
}

.info-item {
    display: flex;
    gap: 20px;
    margin-bottom: 32px;
}

.icon-wrapper {
    flex-shrink: 0;
    width: 48px;
    height: 48px;
    background: white;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
    color: var(--color-primary);
}

.icon {
    width: 24px;
    height: 24px;
    color: #2d5550;
}

.info-content {
    flex: 1;
}

.info-title {
    font-size: 16px;
    font-weight: 600;
    color: #2d5550;
    margin-bottom: 8px;
}

.info-text {
    font-size: 14px;
    color: #5a6a66;
    line-height: 1.6;
    margin-bottom: 2px;
}

.social-links {
    display: flex;
    gap: 16px;
    margin-top: 32px;
}

.social-icon {
    width: 40px;
    height: 40px;
    background: #2d5550;
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    transition: all 0.3s;
    text-decoration: none;
}

.social-icon:hover {
    background: #3d6b64;
    transform: translateY(-2px);
}

.social-icon svg {
    width: 20px;
    height: 20px;
}

.map-container {
    background: #e8f0ef;
    border-radius: 16px;
    overflow: hidden;
    position: relative;
}

.map-placeholder {
    height: 100%;
    min-height: 500px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 40px;
    text-align: center;
}

.map-icon {
    width: 80px;
    height: 80px;
    background: white;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 24px;
    box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
}

.map-icon svg {
    width: 40px;
    height: 40px;
    color: #2d5550;
}

.map-text {
    font-size: 16px;
    color: #2d5550;
    margin-bottom: 24px;
    font-weight: 500;
}

.map-button {
    background: #2d5550;
    color: white;
    border: none;
    border-radius: 10px;
    padding: 14px 32px;
    font-size: 15px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
}

.map-button:hover {
    background: #3d6b64;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(45, 85, 80, 0.3);
}

@media (max-width: 968px) {
    .location-section {
        grid-template-columns: 1fr;
    }

    .map-placeholder {
        min-height: 400px;
    }
}

@media (max-width: 640px) {
    .info-container {
        padding: 30px 24px;
    }

    .section-title {
        font-size: 26px;
        margin-bottom: 30px;
    }

    .info-item {
        gap: 16px;
        margin-bottom: 24px;
    }

    .icon-wrapper {
        width: 40px;
        height: 40px;
    }

    .icon {
        width: 20px;
        height: 20px;
    }

    .map-placeholder {
        min-height: 350px;
        padding: 30px 20px;
    }
}
</style>