<template>
    <div class="page-wrapper">
        <footer class="footer">
            <div class="footer-content">
                
                <!-- Brand Section -->
                <div class="footer-brand">
                    <div class="logo">
                        <img src="../../assets/images/LogoGaia.png" alt="Gaia Estética Animal">
                        <span>Gaia Estética Animal</span>
                    </div>

                    <p class="brand-text">
                        Ofereça seu pet à família. Atendimento profissional com amor
                        e dedicação em cada detalhe.
                    </p>
                </div>

                <!-- Navigation -->
                <div class="footer-section">
                    <h3 class="section-title">Navegação</h3>

                    <ul class="link-list">
                        <li>
                            <RouterLink to="/" class="footer-link">
                                Início
                            </RouterLink>
                        </li>
                        <li>
                            <RouterLink to="/services" class="footer-link">
                                Serviços
                            </RouterLink>
                        </li>
                        <li>
                            <RouterLink to="/about-us" class="footer-link">
                                Sobre nós
                            </RouterLink>
                        </li>
                        <li>
                            <RouterLink to="/contact" class="footer-link">
                                Contato
                            </RouterLink>
                        </li>
                    </ul>
                </div>

                <!-- Business Hours -->
                <div class="footer-section">
                    <h3 class="section-title">Horário de Atendimento</h3>

                    <p class="hours-text">
                        <strong>Terça a Sexta</strong><br />
                        08:00 às 12:00<br />
                        13:30 às 18:00
                    </p>

                    <p class="hours-text">
                        <strong>Sábados</strong><br />
                        08:00 às 13:00
                    </p>
                </div>
            </div>

            <!-- Copyright -->
            <div class="footer-bottom">
                <p class="copyright">
                    © 2024 Gaia Estética Animal. Todos os direitos reservados. <br />
                    Feito e Desenvolvido por
                    <a
                        href="https://my-portfolio-anthonygabriel.vercel.app/"
                        target="_blank"
                        rel="noopener noreferrer"
                        class="developer-link"
                    >
                        Anthony Gabriel
                    </a>
                </p>
            </div>
        </footer>
    </div>
</template>

<script setup>
import { RouterLink } from 'vue-router'
</script>

<style scoped>
.footer {
    background: #2d5550;
    color: white;
    padding: 60px 40px 30px;
    width: 100%;
}

.footer-content {
    display: grid;
    grid-template-columns: 1.5fr 1fr 1.2fr;
    gap: 60px;
    margin-bottom: 50px;
    width: 90%;
    margin: 0 auto 50px;
}

.footer-brand {
    display: flex;
    flex-direction: column;
}

.logo {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 20px;
}

.logo img {
    width: 60px;
    height: 60px;
    object-fit: contain;
    border-radius: 50%;
}

.brand-text {
    font-size: 14px;
    line-height: 1.6;
    color: #e0e0e0;
}

.footer-section {
    display: flex;
    flex-direction: column;
}

.section-title {
    font-size: 16px;
    font-weight: 600;
    margin-bottom: 20px;
    letter-spacing: 0.5px;
}

.link-list {
    list-style: none;
    padding: 0;
    margin: 0;
}

.link-list li {
    margin-bottom: 12px;
}

.footer-link {
    color: #e0e0e0;
    text-decoration: none;
    font-size: 14px;
    transition: color 0.3s ease;
}

.footer-link:hover {
    color: #ffffff;
}

.hours-text {
    font-size: 14px;
    color: #e0e0e0;
    line-height: 1.6;
    margin-bottom: 16px;
}

.footer-bottom {
    border-top: 1px solid rgba(255, 255, 255, 0.1);
    padding-top: 30px;
    text-align: center;
    width: 90%;
    margin: 0 auto;
}

.copyright {
    font-size: 13px;
    color: #b0b0b0;
    line-height: 1.6;
}

.developer-link {
    color: #ffffff;
    font-weight: 600;
    text-decoration: none;
    margin-left: 4px;
    transition: opacity 0.3s ease;
}

.developer-link:hover {
    opacity: 0.8;
    text-decoration: underline;
}

/* Responsive */
@media (max-width: 1024px) {
    .footer-content {
        grid-template-columns: 1fr 1fr;
        gap: 40px;
    }
}

@media (max-width: 640px) {
    .footer {
        padding: 40px 20px 20px;
    }

    .footer-content {
        grid-template-columns: 1fr;
        gap: 30px;
    }
}
</style>
