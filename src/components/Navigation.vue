<!-- src/components/Navigation.vue -->
<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
// import { useTheme } from '../composables/useTheme'

// const { theme, toggleTheme, initTheme } = useTheme()

const isScrolled = ref(false)
const isMenuOpen = ref(false)

const navItems = [
  { href: '#collection', label: 'Коллекция', number: '01' },
  { href: '#about', label: 'О художнике', number: '02' },
  { href: '#contact', label: 'Контакты', number: '03' }
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 40
}

const closeMenu = () => {
  isMenuOpen.value = false
}

onMounted(() => {
  // initTheme()
  window.addEventListener('scroll', handleScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header class="nav" :class="{ 'is-scrolled': isScrolled, 'is-open': isMenuOpen }">
    <div class="container nav__inner">
      <a href="#home" class="nav__logo" @click="closeMenu">
        <span class="nav__logo-mark">ON</span>
        <span class="nav__logo-text">
          <span class="nav__logo-name">Olivia Noir</span>
          <span class="nav__logo-sub">Oil · Art · Gallery</span>
        </span>
      </a>

      <nav class="nav__menu" :class="{ 'is-open': isMenuOpen }">
        <ul class="nav__list">
          <li v-for="item in navItems" :key="item.href">
            <a :href="item.href" class="nav__link" @click="closeMenu">
              <span class="nav__link-num">{{ item.number }}</span>
              <span class="nav__link-label">{{ item.label }}</span>
            </a>
          </li>
        </ul>
      </nav>

      <div class="nav__actions">
        <!-- <button 
          class="nav__theme-toggle"
          @click="toggleTheme"
          :aria-label="theme === 'dark' ? 'Переключить на светлую тему' : 'Переключить на тёмную тему'"
        >
          <svg v-if="theme === 'dark'" width="20" height="20" viewBox="0 0 20 20" fill="none">
            <circle cx="10" cy="10" r="4" stroke="currentColor" stroke-width="1.5"/>
            <path d="M10 2v2M10 16v2M2 10h2M16 10h2M4.93 4.93l1.41 1.41M13.66 13.66l1.41 1.41M4.93 15.07l1.41-1.41M13.66 6.34l1.41-1.41" stroke="currentColor" stroke-width="1.5"/>
          </svg>
          <svg v-else width="20" height="20" viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
            <path d="M17.5 10.5A7.5 7.5 0 1 1 9.5 2.5 5.5 5.5 0 0 0 17.5 10.5z"/>
          </svg>
        </button> -->

        <a href="#contact" class="nav__cta" @click="closeMenu">
          Заказать работу
        </a>

        <button 
          class="nav__burger" 
          :class="{ 'is-open': isMenuOpen }"
          @click="isMenuOpen = !isMenuOpen"
          aria-label="Меню"
          :aria-expanded="isMenuOpen"
        >
          <span></span>
          <span></span>
        </button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  padding: 1.5rem 0;
  transition: all var(--duration-normal) var(--ease-out);
}

.nav.is-scrolled {
  padding: 1rem 0;
  background: rgba(10, 10, 10, 0.85);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--color-line);
}

[data-theme="light"] .nav.is-scrolled {
  background: rgba(250, 248, 245, 0.85);
}

.nav__inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 2rem;
}

.nav__logo {
  display: flex;
  align-items: center;
  gap: 0.875rem;
  color: var(--color-text);
  transition: opacity var(--duration-fast) var(--ease-out);
}

.nav__logo:hover {
  opacity: 0.7;
}

.nav__logo-mark {
  font-family: var(--font-serif);
  font-size: 1.5rem;
  font-weight: 500;
  color: var(--color-accent);
  letter-spacing: 0.05em;
  line-height: 1;
}

.nav__logo-text {
  display: flex;
  flex-direction: column;
  line-height: 1.1;
}

.nav__logo-name {
  font-family: var(--font-serif);
  font-size: 1.125rem;
  font-weight: 500;
  letter-spacing: 0.02em;
}

.nav__logo-sub {
  font-size: 0.6875rem;
  color: var(--color-text-muted);
  letter-spacing: 0.15em;
  text-transform: uppercase;
  margin-top: 0.125rem;
}

.nav__menu {
  flex: 1;
  display: flex;
  justify-content: center;
}

.nav__list {
  display: flex;
  list-style: none;
  gap: 2.5rem;
}

.nav__link {
  display: inline-flex;
  align-items: baseline;
  gap: 0.5rem;
  font-size: 0.875rem;
  color: var(--color-text-muted);
  transition: color var(--duration-fast) var(--ease-out);
  position: relative;
}

.nav__link:hover {
  color: var(--color-text);
}

.nav__link-num {
  font-size: 0.6875rem;
  color: var(--color-accent);
  font-weight: 500;
  letter-spacing: 0.1em;
}

.nav__link::after {
  content: '';
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 0;
  height: 1px;
  background: var(--color-accent);
  transition: width var(--duration-normal) var(--ease-out);
}

.nav__link:hover::after {
  width: 100%;
}

.nav__actions {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.nav__theme-toggle {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-text-muted);
  border: 1px solid var(--color-line);
  border-radius: 50%;
  transition: all var(--duration-fast) var(--ease-out);
}

.nav__theme-toggle:hover {
  color: var(--color-accent);
  border-color: var(--color-accent);
}

.nav__theme-toggle svg {
  transition: transform var(--duration-normal) var(--ease-out);
}

.nav__theme-toggle:hover svg {
  transform: rotate(15deg);
}

.nav__cta {
  font-size: 0.8125rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  padding: 0.75rem 1.5rem;
  border: 1px solid var(--color-line-strong);
  border-radius: 2px;
  color: var(--color-text);
  transition: all var(--duration-fast) var(--ease-out);
}

.nav__cta:hover {
  border-color: var(--color-accent);
  color: var(--color-accent);
}

.nav__burger {
  display: none;
  width: 28px;
  height: 20px;
  position: relative;
  z-index: 101;
}

.nav__burger span {
  position: absolute;
  left: 0;
  width: 100%;
  height: 1px;
  background: var(--color-text);
  transition: all var(--duration-normal) var(--ease-out);
}

.nav__burger span:first-child { top: 4px; }
.nav__burger span:last-child { bottom: 4px; }

.nav__burger.is-open span:first-child {
  top: 50%;
  transform: translateY(-50%) rotate(45deg);
}

.nav__burger.is-open span:last-child {
  bottom: auto;
  top: 50%;
  transform: translateY(-50%) rotate(-45deg);
}

@media (max-width: 900px) {
  .nav__cta { display: none; }
  .nav__burger { display: block; }

  .nav__menu {
    position: fixed;
    inset: 0;
    background: var(--color-bg);
    flex: none;
    justify-content: center;
    align-items: center;
    opacity: 0;
    pointer-events: none;
    transition: opacity var(--duration-normal) var(--ease-out);
  }

  .nav__menu.is-open {
    opacity: 1;
    pointer-events: all;
  }

  .nav__list {
    flex-direction: column;
    gap: 2rem;
    align-items: center;
  }

  .nav__link {
    font-family: var(--font-serif);
    font-size: 2rem;
    color: var(--color-text);
  }

  .nav__link-num {
    font-family: var(--font-sans);
    font-size: 0.75rem;
  }
}
</style>