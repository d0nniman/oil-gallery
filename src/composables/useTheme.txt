// src/composables/useTheme.ts
import { ref, onMounted } from 'vue'

type Theme = 'dark' | 'light'

const THEME_KEY = 'theme'

// Глобальное состояние темы (singleton)
const currentTheme = ref<Theme>('dark')
let isInitialized = false

function getInitialTheme(): Theme {
  // 1. Проверяем localStorage
  const stored = localStorage.getItem(THEME_KEY)
  if (stored === 'dark' || stored === 'light') {
    return stored
  }
  
  // 2. Проверяем системные предпочтения
//   if (window.matchMedia('(prefers-color-scheme: light)').matches) {
//     return 'light'
//   }
  
  // 3. По умолчанию — тёмная
  return 'dark'
}

export function useTheme() {
  function initTheme() {
    if (isInitialized) return
    
    currentTheme.value = getInitialTheme()
    applyTheme(currentTheme.value)
    isInitialized = true
  }
  
  function applyTheme(theme: Theme) {
    document.documentElement.setAttribute('data-theme', theme)
    localStorage.setItem(THEME_KEY, theme)
  }
  
  function toggleTheme() {
    currentTheme.value = currentTheme.value === 'dark' ? 'light' : 'dark'
    applyTheme(currentTheme.value)
  }
  
  function setTheme(theme: Theme) {
    currentTheme.value = theme
    applyTheme(theme)
  }
  
  // Следим за изменениями системной темы
  onMounted(() => {
    const mediaQuery = window.matchMedia('(prefers-color-scheme: dark)')
    
    const handleChange = (e: MediaQueryListEvent) => {
      // Меняем тему только если пользователь не выбрал явно
      if (!localStorage.getItem(THEME_KEY)) {
        currentTheme.value = e.matches ? 'dark' : 'light'
        applyTheme(currentTheme.value)
      }
    }
    
    mediaQuery.addEventListener('change', handleChange)
    
    return () => {
      mediaQuery.removeEventListener('change', handleChange)
    }
  })
  
  return {
    theme: currentTheme,
    toggleTheme,
    setTheme,
    initTheme
  }
}