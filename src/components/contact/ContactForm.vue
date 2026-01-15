<template>
  <section class="contact-form-section">
    <h2 class="section-title">
      <Email :size="28" />
      Agende um Horário
    </h2>
    
    <form @submit.prevent="submitForm" class="contact-form">
      <div class="form-group">
        <label for="nome">Seu Nome Completo</label>
        <div class="input-with-icon">
          <Account :size="20" class="input-icon" />
          <input
            id="nome"
            v-model="formData.nome"
            type="text"
            placeholder="Como seu pet te chama?"
            required
          />
        </div>
      </div>

      <div class="form-group">
        <label for="pet">Nome do seu Pet</label>
        <div class="input-with-icon">
          <Dog :size="20" class="input-icon" />
          <input
            id="pet"
            v-model="formData.pet"
            type="text"
            placeholder="Qual o nome do seu amiguinho?"
            required
          />
        </div>
      </div>

      <div class="form-group">
        <label for="servico">Serviço de Interesse</label>
        <div class="select-with-icon">
          <FormatListBulleted :size="20" class="select-icon" />
          <select
            id="servico"
            v-model="formData.servico"
            required
            class="service-select"
          >
            <option value="" disabled selected>Selecione um serviço</option>
            <option 
              v-for="service in services" 
              :key="service.title" 
              :value="service.whatsappMessage"
            >
              {{ service.title }}
            </option>
          </select>
          <ChevronDown :size="20" class="select-arrow" />
        </div>
      </div>

      <div class="form-group">
        <label for="mensagem">Mensagem Adicional</label>
        <div class="textarea-with-icon">
          <MessageText :size="20" class="textarea-icon" />
          <textarea
            id="mensagem"
            v-model="formData.mensagem"
            placeholder="Conte-nos mais sobre seu pet ou alguma necessidade especial..."
            rows="4"
          ></textarea>
        </div>
      </div>

      <!-- Botão HEADER_CTA Aplicado -->
      <button type="submit" class="header__cta" aria-label="Agendar pelo WhatsApp">
        <WhatsAppIcon class="header__cta-icon" :size="20" />
        <span class="header__cta-text">Agendar pelo WhatsApp</span>
      </button>
    </form>

    <!-- WhatsApp Direct Section -->
    <div class="whatsapp-section">
      <p>Ou se preferir, chame agora no WhatsApp:</p>
      <!-- Botão HEADER_CTA para WhatsApp direto -->
      <button class="header__cta" aria-label="Conversar agora no WhatsApp" @click="handleWhatsAppDirect">
        <WhatsAppIcon class="header__cta-icon" :size="20" />
        <span class="header__cta-text">Conversar agora</span>
      </button>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import { services } from '@/data/services'

import Email from 'vue-material-design-icons/Email.vue'
import Account from 'vue-material-design-icons/Account.vue'
import Dog from 'vue-material-design-icons/Dog.vue'
import FormatListBulleted from 'vue-material-design-icons/FormatListBulleted.vue'
import ChevronDown from 'vue-material-design-icons/ChevronDown.vue'
import MessageText from 'vue-material-design-icons/MessageText.vue'
import WhatsAppIcon from 'vue-material-design-icons/Whatsapp.vue'

const phoneNumber = '+554796180343'

const formData = ref({
  nome: '',
  pet: '',
  servico: '',
  mensagem: ''
})

// Função para WhatsApp direto (sem formulário)
const handleWhatsAppDirect = () => {
  const baseMessage = `Olá! Gostaria de saber mais sobre os serviços da Gaia Estética Animal.`
  const encodedMessage = encodeURIComponent(baseMessage)
  const whatsappUrl = `https://wa.me/${phoneNumber}?text=${encodedMessage}`
  window.open(whatsappUrl, '_blank')
}

// Função para gerar a mensagem completa do WhatsApp
const generateWhatsAppMessage = () => {
  const selectedService = services.find(s => s.whatsappMessage === formData.value.servico)
  const serviceTitle = selectedService ? selectedService.title : 'um serviço'
  
  let message = `Olá! Me chamo *${formData.value.nome}* e gostaria de marcar um horário ou saber sobre *${serviceTitle}* para meu pet *${formData.value.pet}*.`
  
  if (formData.value.mensagem) {
    message += `\n\nMensagem adicional:\n${formData.value.mensagem}`
  }
  
  return encodeURIComponent(message)
}

const submitForm = () => {
  if (!formData.value.servico) {
    alert('Por favor, selecione um serviço de interesse')
    return
  }
  
  // Gerar mensagem para WhatsApp
  const whatsappMessage = generateWhatsAppMessage()
  const whatsappUrl = `https://wa.me/${phoneNumber}?text=${whatsappMessage}`
  
  // Abrir WhatsApp em nova aba
  window.open(whatsappUrl, '_blank')
  
  // Log para desenvolvimento
  console.log('Form submitted:', formData.value)
  console.log('WhatsApp URL:', whatsappUrl)
  
  // Reset form
  formData.value = {
    nome: '',
    pet: '',
    servico: '',
    mensagem: ''
  }
}
</script>

<style scoped>
.contact-form-section {
  background: rgba(255, 255, 255, 0.5);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 24px;
  padding: 32px;
  box-shadow: 0 20px 40px rgba(25, 64, 49, 0.05);
}

.dark .contact-form-section {
  background: rgba(31, 41, 55, 0.4);
  border-color: rgba(55, 65, 81, 0.3);
}

.section-title {
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 24px;
  display: flex;
  align-items: center;
  gap: 12px;
  color: #194031;
}

.dark .section-title {
  color: #D19CA4;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-bottom: 32px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  font-size: 0.875rem;
  font-weight: 600;
  margin-bottom: 8px;
  margin-left: 4px;
  color: #194031;
}

.dark .form-group label {
  color: #D19CA4;
}

/* Input with icon */
.input-with-icon,
.select-with-icon,
.textarea-with-icon {
  position: relative;
  display: flex;
  align-items: center;
}

.input-icon,
.select-icon,
.textarea-icon {
  position: absolute;
  left: 16px;
  color: #194031;
  z-index: 1;
}

.dark .input-icon,
.dark .select-icon,
.dark .textarea-icon {
  color: #D19CA4;
}

.form-group input,
.form-group textarea,
.service-select {
  padding: 16px 16px 16px 48px;
  border: 1px solid rgba(209, 213, 219, 0.3);
  border-radius: 16px;
  background: rgba(249, 250, 251, 0.8);
  font-size: 1rem;
  transition: all 0.3s ease;
  font-family: inherit;
  width: 100%;
}

.dark .form-group input,
.dark .form-group textarea,
.dark .service-select {
  background: rgba(17, 24, 39, 0.7);
  border-color: rgba(55, 65, 81, 0.3);
  color: #F2EBC4;
}

/* Select specific styles */
.select-with-icon {
  position: relative;
}

.service-select {
  appearance: none;
  padding-right: 48px;
  cursor: pointer;
}

.select-arrow {
  position: absolute;
  right: 16px;
  color: #194031;
  pointer-events: none;
}

.dark .select-arrow {
  color: #D19CA4;
}

/* Textarea specific styles */
.textarea-with-icon {
  align-items: flex-start;
}

.textarea-icon {
  margin-top: 16px;
}

textarea {
  resize: vertical;
  min-height: 120px;
}

/* Focus states */
.service-select:focus,
.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #194031;
  box-shadow: 0 0 0 3px rgba(25, 64, 49, 0.1);
}

.dark .service-select:focus,
.dark .form-group input:focus,
.dark .form-group textarea:focus {
  border-color: #D19CA4;
  box-shadow: 0 0 0 3px rgba(209, 156, 164, 0.2);
}

/* Placeholder styles */
.form-group input::placeholder,
.form-group textarea::placeholder,
.service-select:invalid {
  color: rgba(107, 114, 128, 0.7);
}

.dark .form-group input::placeholder,
.dark .form-group textarea::placeholder,
.dark .service-select:invalid {
  color: rgba(156, 163, 175, 0.7);
}

/* ============= HEADER_CTA STYLES ============= */
.header__cta {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.875rem 1.75rem;
  border-radius: 50px;
  border: 0;
  background-color: #194031; /* var(--color-primary) */
  color: white;
  font-family: 'Lexend', sans-serif;
  font-weight: 700;
  font-size: 0.95rem;
  cursor: pointer;
  transition: all 0.3s ease;
  white-space: nowrap;
  flex-shrink: 0;
  width: 100%;
  margin-top: 8px;
}

.header__cta:hover {
  background-color: #143028; /* var(--color-accent) mais escuro */
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(31, 77, 63, 0.2);
}

.header__cta:active {
  transform: translateY(0);
}

.header__cta-icon {
  display: flex;
  align-items: center;
  justify-content: center;
}

/* WhatsApp section */
.whatsapp-section {
  padding-top: 32px;
  border-top: 1px solid rgba(209, 213, 219, 0.3);
}

.dark .whatsapp-section {
  border-top-color: rgba(55, 65, 81, 0.3);
}

.whatsapp-section p {
  text-align: center;
  color: rgba(107, 114, 128, 0.9);
  font-size: 0.875rem;
  margin-bottom: 16px;
}

.dark .whatsapp-section p {
  color: rgba(156, 163, 175, 0.9);
}

/* Responsive */
@media (max-width: 768px) {
  .contact-form-section {
    padding: 24px;
  }
  
  .section-title {
    font-size: 1.5rem;
  }
  
  .header__cta {
    padding: 0.875rem 1.5rem;
    font-size: 0.9rem;
  }
}

@media (max-width: 480px) {
  .contact-form-section {
    padding: 20px;
  }
  
  .form-group input,
  .form-group textarea,
  .service-select {
    padding: 14px 14px 14px 44px;
  }
  
  .input-icon,
  .select-icon,
  .textarea-icon {
    left: 14px;
  }
  
  .select-arrow {
    right: 14px;
  }
  
  .header__cta {
    padding: 0.875rem 1.25rem;
    font-size: 0.85rem;
  }
}

@media (max-width: 1024px) {
  .header__cta {
    width: 100%;
    align-items: center;
    justify-content: center;
  }
}

span{
    display: flex;
    align-items: center;
    justify-content: center;
}

/* Adicione isso no final do ContactForm.vue */
@media screen and (max-width: 480px) {
  .contact-form-section {
    padding: 20px 16px; /* Reduz padding horizontal em mobile */
    margin: 0 -8px; /* Compensa o padding do container pai */
  }
  
  .section-title {
    font-size: 1.4rem;
    flex-wrap: wrap;
  }
  
  .form-group input,
  .form-group textarea,
  .service-select {
    padding: 14px 12px 14px 42px;
    font-size: 0.95rem;
  }
  
  .input-icon,
  .select-icon,
  .textarea-icon {
    left: 12px;
  }
  
  .select-arrow {
    right: 12px;
  }
  
  .header__cta {
    padding: 0.875rem 1rem;
    font-size: 0.85rem;
    white-space: normal; /* Permite quebra de texto */
  }
  
  .header__cta-text {
    text-align: center;
  }
}

@media screen and (max-width: 360px) {
  .contact-form-section {
    padding: 16px 12px;
    margin: 0 -6px;
  }
  
  .section-title {
    font-size: 1.2rem;
  }
  
  .form-group input,
  .form-group textarea,
  .service-select {
    padding: 12px 10px 12px 40px;
    font-size: 0.9rem;
  }
  
  .header__cta {
    padding: 0.75rem 0.875rem;
    font-size: 0.8rem;
  }
}
</style>