<!-- src/components/ContactSection.vue -->
<script setup lang="ts">
import { ref, computed } from 'vue'

const form = ref({
  name: '',
  email: '',
  painting: '',
  message: ''
})

const errors = ref<Record<string, string>>({})
const isSubmitting = ref(false)
const isSubmitted = ref(false)

const sanitize = (value: string): string =>
  value.replace(/[<>"'`]/g, '').replace(/javascript:/gi, '').trim()

const validateEmail = (email: string): boolean =>
  /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)

const validate = (): boolean => {
  errors.value = {}
  const name = sanitize(form.value.name)
  const email = sanitize(form.value.email)
  const message = sanitize(form.value.message)

  if (name.length < 2) errors.value.name = 'Укажите имя'
  if (!validateEmail(email)) errors.value.email = 'Некорректный email'
  if (message.length < 5) errors.value.message = 'Слишком короткое сообщение'

  return Object.keys(errors.value).length === 0
}

const submit = async () => {
  if (!validate()) return
  isSubmitting.value = true

  const name = sanitize(form.value.name)
  const email = sanitize(form.value.email)
  const painting = sanitize(form.value.painting)
  const message = sanitize(form.value.message)

  const subject = encodeURIComponent(`Заявка с сайта: ${name}`)
  const body = encodeURIComponent(
    `Имя: ${name}\nEmail: ${email}\nИнтересует работа: ${painting || '—'}\n\n${message}`
  )

  window.location.href = `mailto:gallery@olivianoir.art?subject=${subject}&body=${body}`

  setTimeout(() => {
    isSubmitting.value = false
    isSubmitted.value = true
    form.value = { name: '', email: '', painting: '', message: '' }
    setTimeout(() => (isSubmitted.value = false), 5000)
  }, 300)
}

// const hasError = (field: string) => computed(() => !!errors.value[field])
</script>

<template>
  <section id="contact" class="contact">
    <div class="container contact__inner">
      <div class="contact__info reveal">
        <span class="overline">Связаться</span>
        <h2 class="contact__title">
          Готовы обсудить<br />
          <em>приобретение работы?</em>
        </h2>
        <p class="contact__description">
          Напишите или позвоните — расскажу о доступных картинах, 
          условиях доставки и оформления. Отвечаю в течение дня.
        </p>

        <div class="contact__methods">
          <a href="tel:+79991234567" class="contact__method">
            <span class="contact__method-label">Телефон</span>
            <span class="contact__method-value">+7 (999) 123-45-67</span>
          </a>
          <a href="mailto:gallery@olivianoir.art" class="contact__method">
            <span class="contact__method-label">Email</span>
            <span class="contact__method-value">gallery@olivianoir.art</span>
          </a>
          <div class="contact__method">
            <span class="contact__method-label">Мастерская</span>
            <span class="contact__method-value">Москва, по записи</span>
          </div>
        </div>
      </div>

      <form class="contact__form reveal" @submit.prevent="submit" novalidate>
        <div class="form__field" :class="{ 'has-error': errors.name }">
          <label for="name">Имя</label>
          <input 
            id="name" 
            v-model="form.name" 
            type="text" 
            maxlength="100" 
            autocomplete="name"
            placeholder="Ваше имя"
          />
          <span v-if="errors.name" class="form__error">{{ errors.name }}</span>
        </div>

        <div class="form__field" :class="{ 'has-error': errors.email }">
          <label for="email">Email</label>
          <input 
            id="email" 
            v-model="form.email" 
            type="email" 
            maxlength="100" 
            autocomplete="email"
            placeholder="you@example.com"
          />
          <span v-if="errors.email" class="form__error">{{ errors.email }}</span>
        </div>

        <div class="form__field">
          <label for="painting">Интересует работа <span class="optional">(необязательно)</span></label>
          <input 
            id="painting" 
            v-model="form.painting" 
            type="text" 
            maxlength="100"
            placeholder="Например: «Тихий вечер»"
          />
        </div>

        <div class="form__field" :class="{ 'has-error': errors.message }">
          <label for="message">Сообщение</label>
          <textarea 
            id="message" 
            v-model="form.message" 
            rows="4" 
            maxlength="1000"
            placeholder="Ваш вопрос или пожелания"
          ></textarea>
          <span v-if="errors.message" class="form__error">{{ errors.message }}</span>
        </div>

        <button type="submit" class="form__submit" :disabled="isSubmitting">
          <span v-if="isSubmitting">Отправка…</span>
          <span v-else>
            Отправить заявку
            <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
              <path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" stroke-width="1.5"/>
            </svg>
          </span>
        </button>

        <Transition name="fade">
          <p v-if="isSubmitted" class="form__success">
            Спасибо. Письмо откроется в вашем почтовом клиенте.
          </p>
        </Transition>
      </form>
    </div>
  </section>
</template>

<style scoped>
.contact {
  padding: clamp(4rem, 10vw, 8rem) 0;
  background: var(--color-bg);
  border-top: 1px solid var(--color-line);
}

.contact__inner {
  display: grid;
  grid-template-columns: 1fr 1.1fr;
  gap: clamp(2rem, 6vw, 6rem);
  align-items: start;
}

.contact__title {
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 300;
  line-height: 1.1;
  margin: 1.5rem 0 1.5rem;
}

.contact__title em {
  font-style: italic;
  color: var(--color-accent);
}

.contact__description {
  color: var(--color-text-muted);
  font-size: 1.0625rem;
  line-height: 1.7;
  max-width: 440px;
  margin-bottom: 3rem;
}

.contact__methods {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  padding-top: 2rem;
  border-top: 1px solid var(--color-line);
}

.contact__method {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  transition: color var(--duration-fast) var(--ease-out);
}

a.contact__method:hover .contact__method-value {
  color: var(--color-accent);
}

.contact__method-label {
  font-size: 0.6875rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-text-dim);
}

.contact__method-value {
  font-family: var(--font-serif);
  font-size: 1.375rem;
  color: var(--color-text);
  transition: color var(--duration-fast) var(--ease-out);
}

/* Form */
.contact__form {
  background: var(--color-bg-elevated);
  padding: clamp(1.5rem, 3vw, 2.5rem);
  border: 1px solid var(--color-line);
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form__field {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form__field label {
  font-size: 0.75rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-text-muted);
}

.optional {
  color: var(--color-text-dim);
  text-transform: none;
  letter-spacing: normal;
  font-size: 0.75rem;
}

.form__field input,
.form__field textarea {
  background: transparent;
  border: none;
  border-bottom: 1px solid var(--color-line-strong);
  padding: 0.75rem 0;
  color: var(--color-text);
  font-family: inherit;
  font-size: 1rem;
  font-weight: 300;
  transition: border-color var(--duration-fast) var(--ease-out);
  resize: vertical;
}

.form__field input::placeholder,
.form__field textarea::placeholder {
  color: var(--color-text-dim);
}

.form__field input:focus,
.form__field textarea:focus {
  outline: none;
  border-bottom-color: var(--color-accent);
}

.form__field.has-error input,
.form__field.has-error textarea {
  border-bottom-color: #c97a7a;
}

.form__error {
  font-size: 0.8125rem;
  color: #c97a7a;
  margin-top: 0.25rem;
}

.form__submit {
  margin-top: 0.5rem;
  padding: 1.125rem 2rem;
  background: var(--color-text);
  color: var(--color-bg);
  font-size: 0.875rem;
  font-weight: 500;
  letter-spacing: 0.05em;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  transition: all var(--duration-normal) var(--ease-out);
  border-radius: 2px;
}

.form__submit:hover:not(:disabled) {
  background: var(--color-accent);
}

.form__submit:hover:not(:disabled) svg {
  transform: translateX(4px);
}

.form__submit svg {
  transition: transform var(--duration-normal) var(--ease-out);
}

.form__submit:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.form__success {
  padding: 1rem;
  background: rgba(184, 147, 90, 0.08);
  border: 1px solid var(--color-accent-dim);
  color: var(--color-accent);
  font-size: 0.875rem;
  text-align: center;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity var(--duration-normal) var(--ease-out);
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 900px) {
  .contact__inner {
    grid-template-columns: 1fr;
  }
}
</style>