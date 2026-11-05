<!-- src/components/GallerySection.vue -->
<script setup lang="ts">
import { ref } from 'vue'

interface Painting {
  id: number
  title: string
  year: string
  technique: string
  size: string
  price: string
  image: string
  category: string
}

const paintings = ref<Painting[]>([
  {
    id: 1,
    title: 'Тихий вечер',
    year: '2024',
    technique: 'Нефть, масло на холсте',
    size: '80 × 100 см',
    price: '85 000 ₽',
    image: 'https://images.unsplash.com/photo-1578926288207-a90a5366759d?w=800&q=80',
    category: 'Пейзаж'
  },
  {
    id: 2,
    title: 'Чёрное золото',
    year: '2024',
    technique: 'Нефть, акрил на холсте',
    size: '100 × 120 см',
    price: '120 000 ₽',
    image: 'https://images.unsplash.com/photo-1549887534-1541e9326642?w=800&q=80',
    category: 'Абстракция'
  },
  {
    id: 3,
    title: 'Северное сияние',
    year: '2023',
    technique: 'Нефть, масло на холсте',
    size: '90 × 90 см',
    price: '95 000 ₽',
    image: 'https://images.unsplash.com/photo-1579783902614-a3fb3927b6a5?w=800&q=80',
    category: 'Пейзаж'
  },
  {
    id: 4,
    title: 'Память воды',
    year: '2024',
    technique: 'Нефть, масло на холсте',
    size: '70 × 90 см',
    price: '72 000 ₽',
    image: 'https://images.unsplash.com/photo-1547891654-e66ed7ebb968?w=800&q=80',
    category: 'Абстракция'
  },
  {
    id: 5,
    title: 'Рассвет в тумане',
    year: '2023',
    technique: 'Нефть, масло на холсте',
    size: '60 × 80 см',
    price: '65 000 ₽',
    image: 'https://images.unsplash.com/photo-1578321272176-b7bbc0679853?w=800&q=80',
    category: 'Пейзаж'
  },
  {
    id: 6,
    title: 'Грани времени',
    year: '2024',
    technique: 'Нефть, смешанная техника',
    size: '100 × 100 см',
    price: '140 000 ₽',
    image: 'https://images.unsplash.com/photo-1574182245530-967d9b3831af?w=800&q=80',
    category: 'Абстракция'
  }
])

const selected = ref<Painting | null>(null)

const openModal = (p: Painting) => {
  selected.value = p
  document.body.style.overflow = 'hidden'
}

const closeModal = () => {
  selected.value = null
  document.body.style.overflow = ''
}
</script>

<template>
  <section id="collection" class="collection">
    <div class="container">
      <header class="collection__header reveal">
        <div class="collection__header-top">
          <span class="overline">Коллекция · 2024</span>
          <span class="collection__count">06 работ</span>
        </div>
        <h2 class="collection__title">
          Избранные работы<br />
          <em>из мастерской</em>
        </h2>
        <p class="collection__description">
          Каждая картина — результат месяцев работы с материалом. 
          Нефть придаёт полотнам глубину, которую невозможно повторить 
          традиционными красками.
        </p>
      </header>

      <div class="collection__grid">
        <article 
          v-for="painting in paintings" 
          :key="painting.id"
          class="card reveal"
          @click="openModal(painting)"
          tabindex="0"
          @keydown.enter.prevent="openModal(painting)"
        >
          <div class="card__image-wrap">
            <img 
              :src="painting.image" 
              :alt="painting.title"
              class="card__image"
              loading="lazy"
            />
            <span class="card__tag">{{ painting.category }}</span>
          </div>
          <div class="card__info">
            <div class="card__meta">
              <span class="card__number">№ {{ String(painting.id).padStart(2, '0') }}</span>
              <span class="card__year">{{ painting.year }}</span>
            </div>
            <h3 class="card__title">{{ painting.title }}</h3>
            <div class="card__footer">
              <span class="card__size">{{ painting.size }}</span>
              <span class="card__price">{{ painting.price }}</span>
            </div>
          </div>
        </article>
      </div>
    </div>

    <Teleport to="body">
      <Transition name="modal">
        <div v-if="selected" class="modal" @click.self="closeModal">
          <div class="modal__content">
            <button class="modal__close" @click="closeModal" aria-label="Закрыть">
              <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
                <path d="M4 4l12 12M16 4L4 16" stroke="currentColor" stroke-width="1.5"/>
              </svg>
            </button>

            <div class="modal__grid">
              <div class="modal__image-wrap">
                <img :src="selected.image" :alt="selected.title" class="modal__image" />
              </div>
              <div class="modal__info">
                <span class="overline">Работа № {{ String(selected.id).padStart(2, '0') }}</span>
                <h3 class="modal__title">{{ selected.title }}</h3>
                <p class="modal__year">{{ selected.year }}</p>

                <dl class="modal__details">
                  <div>
                    <dt>Техника</dt>
                    <dd>{{ selected.technique }}</dd>
                  </div>
                  <div>
                    <dt>Размер</dt>
                    <dd>{{ selected.size }}</dd>
                  </div>
                  <div>
                    <dt>Стоимость</dt>
                    <dd class="modal__price">{{ selected.price }}</dd>
                  </div>
                </dl>

                <div class="modal__actions">
                  <a href="tel:+79991234567" class="btn btn--primary">
                    Позвонить
                  </a>
                  <a href="mailto:gallery@olivianoir.art" class="btn btn--ghost">
                    Написать
                  </a>
                </div>

                <p class="modal__note">
                  Работа существует в единственном экземпляре. 
                  Доставка по всему миру, оформление в багет.
                </p>
              </div>
            </div>
          </div>
        </div>
      </Transition>
    </Teleport>
  </section>
</template>

<style scoped>
.collection {
  padding: clamp(4rem, 10vw, 8rem) 0;
  background: var(--color-bg);
}

.collection__header {
  margin-bottom: clamp(3rem, 6vw, 5rem);
  max-width: 900px;
}

.collection__header-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
}

.collection__count {
  font-size: 0.75rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-text-dim);
}

.collection__title {
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 300;
  line-height: 1.1;
  margin-bottom: 1.5rem;
}

.collection__title em {
  font-style: italic;
  color: var(--color-accent);
}

.collection__description {
  font-size: 1.0625rem;
  color: var(--color-text-muted);
  max-width: 560px;
  line-height: 1.7;
}

.collection__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: clamp(1.5rem, 3vw, 2.5rem);
}

.card {
  cursor: pointer;
  transition: transform var(--duration-normal) var(--ease-out);
  outline: none;
}

.card:focus-visible .card__image-wrap {
  outline: 2px solid var(--color-accent);
  outline-offset: 4px;
}

.card:hover {
  transform: translateY(-4px);
}

.card__image-wrap {
  position: relative;
  aspect-ratio: 3 / 4;
  overflow: hidden;
  background: var(--color-bg-warm);
  margin-bottom: 1.25rem;
}

.card__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 1s var(--ease-out), filter var(--duration-normal) var(--ease-out);
  filter: saturate(0.85) contrast(1.05);
}

.card:hover .card__image {
  transform: scale(1.04);
  filter: saturate(1) contrast(1.05);
}

.card__tag {
  position: absolute;
  top: 1rem;
  left: 1rem;
  padding: 0.375rem 0.75rem;
  background: rgba(10, 10, 10, 0.8);
  backdrop-filter: blur(10px);
  font-size: 0.6875rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-text);
  border: 1px solid var(--color-line);
}

[data-theme="light"] .card__tag {
  background: rgba(250, 248, 245, 0.9);
}

.card__info {
  padding: 0 0.25rem;
}

.card__meta {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-text-dim);
}

.card__number {
  color: var(--color-accent);
}

.card__title {
  font-family: var(--font-serif);
  font-size: 1.5rem;
  font-weight: 400;
  margin-bottom: 1rem;
  line-height: 1.2;
}

.card__footer {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  padding-top: 1rem;
  border-top: 1px solid var(--color-line);
  font-size: 0.875rem;
}

.card__size {
  color: var(--color-text-muted);
}

.card__price {
  color: var(--color-text);
  font-weight: 500;
  letter-spacing: 0.02em;
}

/* Modal */
.modal {
  position: fixed;
  inset: 0;
  background: rgba(10, 10, 10, 0.92);
  backdrop-filter: blur(20px);
  z-index: 200;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  overflow-y: auto;
}

[data-theme="light"] .modal {
  background: rgba(250, 248, 245, 0.92);
}

.modal__content {
  background: var(--color-bg-elevated);
  max-width: 1100px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  border: 1px solid var(--color-line);
}

.modal__close {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-text);
  z-index: 2;
  transition: color var(--duration-fast) var(--ease-out);
}

.modal__close:hover {
  color: var(--color-accent);
}

.modal__grid {
  display: grid;
  grid-template-columns: 1.2fr 1fr;
}

.modal__image-wrap {
  aspect-ratio: 4 / 5;
  background: var(--color-bg-warm);
}

.modal__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.modal__info {
  padding: clamp(2rem, 4vw, 3.5rem);
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.modal__title {
  font-size: clamp(2rem, 3.5vw, 2.75rem);
  font-weight: 400;
  line-height: 1.1;
  margin-top: 1rem;
}

.modal__year {
  color: var(--color-text-muted);
  font-size: 0.875rem;
  letter-spacing: 0.1em;
}

.modal__details {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  padding: 1.5rem 0;
  border-top: 1px solid var(--color-line);
  border-bottom: 1px solid var(--color-line);
}

.modal__details > div {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 1rem;
}

.modal__details dt {
  font-size: 0.75rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-text-dim);
}

.modal__details dd {
  color: var(--color-text);
  font-size: 0.9375rem;
}

.modal__price {
  color: var(--color-accent);
  font-family: var(--font-serif);
  font-size: 1.5rem;
}

.modal__actions {
  display: flex;
  gap: 0.75rem;
  flex-wrap: wrap;
}

.modal__actions .btn {
  flex: 1;
  justify-content: center;
  min-width: 140px;
}

.modal__note {
  font-size: 0.8125rem;
  color: var(--color-text-muted);
  line-height: 1.6;
  padding-top: 1rem;
  border-top: 1px solid var(--color-line);
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity var(--duration-normal) var(--ease-out);
}

.modal-enter-active .modal__content,
.modal-leave-active .modal__content {
  transition: transform var(--duration-normal) var(--ease-out),
              opacity var(--duration-normal) var(--ease-out);
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal__content,
.modal-leave-to .modal__content {
  transform: translateY(20px);
  opacity: 0;
}

@media (max-width: 1024px) {
  .collection__grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 700px) {
  .collection__grid {
    grid-template-columns: 1fr;
  }

  .modal__grid {
    grid-template-columns: 1fr;
  }

  .modal__image-wrap {
    aspect-ratio: 4 / 3;
  }

  .modal {
    padding: 0;
  }

  .modal__content {
    max-height: 100vh;
    border: none;
  }
}
</style>