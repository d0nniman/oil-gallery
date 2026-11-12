<!-- src/components/DimensionBadge.vue -->
<script setup lang="ts">
defineProps<{
  width: number | string
  height: number | string
  unit?: string
}>()
</script>

<template>
  <div class="dimension-badge">
    <!-- Диагональная линия через SVG для идеальной точности -->
    <svg class="dimension-badge__line" viewBox="0 0 100 100" preserveAspectRatio="none">
      <line x1="0" y1="0" x2="100" y2="100" stroke="var(--color-accent)" stroke-width="1" />
    </svg>

    <!-- Основной размер по центру -->
    <span class="dimension-badge__value">{{ width }} × {{ height }}</span>

    <!-- Единица измерения, разрывающая нижнюю границу -->
    <span class="dimension-badge__unit">{{ unit }}</span>
  </div>
</template>

<style scoped>
.dimension-badge {
  position: relative;
  width: 85px;
  height: 85px;
  border: 1px solid var(--color-accent);
  display: flex;
  align-items: center;
  justify-content: center;
  /* Фон нужен, чтобы текст перекрывал линию и создавал эффект "разрыва" */
  background-color: var(--color-bg-elevated); 
  flex-shrink: 0;
}

.dimension-badge__line {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.dimension-badge__value {
  position: relative;
  z-index: 1;
  /* font-family: var(--font-serif); */
  font-size: .9rem;
  font-weight: 300;
  color: var(--color-text);
  /* Небольшой фон вокруг цифр, чтобы диагональ не мешала чтению */
  background-color: var(--color-bg-elevated);
  padding: 0 6px;
  line-height: 1;
  letter-spacing: 0.02em;
}

.dimension-badge__unit {
  position: absolute;
  bottom: -0.5rem; /* Сдвигаем вниз, чтобы сесть на линию */
  left: 50%;
  transform: translateX(-50%);
  font-family: var(--font-sans);
  font-size: 0.6875rem;
  font-weight: 500;
  color: var(--color-accent);
  letter-spacing: 0.15em;
  text-transform: uppercase;
  line-height: 1;
  /* Фон перекрывает нижнюю границу квадрата, создавая эффект разрыва */
  background-color: var(--color-bg-elevated);
  padding: 0 8px;
}
</style>