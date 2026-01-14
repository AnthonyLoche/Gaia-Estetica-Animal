<template>
  <div class="service-card">
    <div class="icon-wrapper" :class="variant">
      <slot name="icon" />
    </div>

    <h3 class="service-title">{{ title }}</h3>

    <p class="service-description">
      {{ description }}
    </p>

    <a :href="link" class="service-link">
      {{ linkText }} →
    </a>
  </div>
</template>

<script setup>
defineProps({
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  },
  link: {
    type: String,
    default: '#'
  },
  linkText: {
    type: String,
    default: 'SAIBA MAIS'
  },
  variant: {
    type: String,
    default: 'pink'
  }
});
</script>

<style scoped>
.service-card {
  background: white;
  border-radius: 16px;
  padding: 32px 24px;
  text-align: center;
  transition: all 0.3s ease;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.service-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.1);
}

.icon-wrapper {
  width: 64px;
  height: 64px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
  transition: transform 0.3s ease;
}

.service-card:hover .icon-wrapper {
  transform: scale(1.1);
}

.icon-wrapper.pink {
  background: #f8e8f0;
}

.icon-wrapper.green,
.icon-wrapper.dark-green {
  background: #2d5550;
}

/* garante tamanho padrão pros ícones */
.icon-wrapper :deep(svg) {
  width: 32px;
  height: 32px;
}

.icon-wrapper.pink :deep(svg) {
  color: #d4789d;
}

.icon-wrapper.green :deep(svg),
.icon-wrapper.dark-green :deep(svg) {
  color: white;
}

.service-title {
  font-size: 20px;
  font-weight: 700;
  color: #2d3c38;
  margin-bottom: 12px;
}

.service-description {
  font-size: 14px;
  color: #5a6a66;
  line-height: 1.6;
  margin-bottom: 20px;
  flex-grow: 1;
}

.service-link {
  font-size: 13px;
  font-weight: 700;
  color: #2d5550;
  text-decoration: none;
  letter-spacing: 0.5px;
  transition: all 0.3s;
  display: inline-flex;
  align-items: center;
  gap: 4px;
}

.service-link:hover {
  color: #3d6b64;
  gap: 8px;
}
</style>
