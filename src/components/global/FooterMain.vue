<template>
    <div class="page-wrapper">
        <footer class="footer">
            <div class="footer-content">
                <!-- Brand Section -->
                <div class="footer-brand">
                    <div class="logo">
                        <img src="../../assets/images/LogoGaia.png" alt="">
                        Gaia Estética Animal
                    </div>
                    <p class="brand-text">
                        Ofereça seu pet à família. Atendimento profissional com amor e dedicação em cada detalhe.
                    </p>
                </div>

                <!-- Navigation -->
                <div class="footer-section">
                    <h3 class="section-title">Navegação</h3>
                    <ul class="link-list">
                        <li><a href="#" class="footer-link">Início</a></li>
                        <li><a href="#" class="footer-link">Serviços</a></li>
                        <li><a href="#" class="footer-link">Sobre</a></li>
                        <li><a href="#" class="footer-link">Contato</a></li>
                    </ul>
                </div>

                <!-- Policies -->
                <div class="footer-section">
                    <h3 class="section-title">Políticas</h3>
                    <ul class="link-list">
                        <li><a href="#" class="footer-link">Termos de Uso</a></li>
                        <li><a href="#" class="footer-link">Privacidade</a></li>
                        <li><a href="#" class="footer-link">Cuidados Pós-Banho</a></li>
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
                    © 2024 Gaia Estética Animal. Todos os direitos reservados.
                    Feito com <span class="heart">❤</span> para o seu pet
                </p>
            </div>
        </footer>
    </div>
</template>

<script setup>
</script>

<style scoped>
.footer {
    background: #2d5550;
    color: white;
    padding: 60px 40px 30px;
    width: 100%;
    margin: 0 auto;
}

.footer-content {
    display: grid;
    grid-template-columns: 1.5fr 1fr 1fr 1.2fr;
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
    width: 60px;
    height: 60px;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 1rem;
}

.logo img {
    width: 100%;
    height: 100%;
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
    transition: color 0.3s;
}

.footer-link:hover {
    color: #fff;
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
}

.heart {
    color: #ff6b6b;
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
