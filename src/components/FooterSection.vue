<!-- src/components/FooterSection.vue -->
<template>
  <footer class="footer">
    <div class="container footer__inner">
      <div class="footer__brand">
        <div class="footer__logo">
          <span class="footer__logo-mark">ON</span>
          <div class="footer__logo-text">
            <span class="footer__logo-name">Olivia Noir</span>
            <span class="footer__logo-sub">Oil · Art · Gallery</span>
          </div>
        </div>
        <p class="footer__tagline">
          Авторская галерея картин,<br />
          написанных нефтью.
        </p>
      </div>

      <nav class="footer__nav">
        <h4 class="footer__heading">Навигация</h4>
        <ul>
          <li><a href="#collection">Коллекция</a></li>
          <li><a href="#about">О художнике</a></li>
          <li><a href="#contact">Контакты</a></li>
        </ul>
      </nav>

      <div class="footer__contact">
        <h4 class="footer__heading">Связаться</h4>
        <ul>
          <li><a href="tel:+79991234567">+7 (999) 123-45-67</a></li>
          <li><a href="mailto:gallery@olivianoir.art">gallery@olivianoir.art</a></li>
          <li>Москва, по записи</li>
        </ul>
      </div>

      <div class="footer__legal">
        <h4 class="footer__heading">Информация</h4>
        <ul>
          <li>Доставка по всему миру</li>
          <li>Оформление в багет</li>
          <li>Сертификат подлинности</li>
        </ul>
      </div>
    </div>

    <div class="footer__bottom">
      <div class="container footer__bottom-inner">
        <span>© 2026 Olivia Noir. Все работы авторские.</span>
        <span class="footer__made">Сделано с вниманием к деталям</span>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: var(--color-bg-elevated);
  border-top: 1px solid var(--color-line);
  padding-top: clamp(3rem, 6vw, 5rem);
}

.footer__inner {
  display: grid;
  grid-template-columns: 1.5fr 1fr 1fr 1fr;
  gap: clamp(2rem, 4vw, 3rem);
  padding-bottom: clamp(3rem, 6vw, 5rem);
}

.footer__logo {
  display: flex;
  align-items: center;
  gap: 0.875rem;
  margin-bottom: 1.5rem;
}

.footer__logo-mark {
  font-family: var(--font-serif);
  font-size: 1.5rem;
  color: var(--color-accent);
  letter-spacing: 0.05em;
}

.footer__logo-text {
  display: flex;
  flex-direction: column;
  line-height: 1.1;
}

.footer__logo-name {
  font-family: var(--font-serif);
  font-size: 1.125rem;
}

.footer__logo-sub {
  font-size: 0.6875rem;
  color: var(--color-text-muted);
  letter-spacing: 0.15em;
  text-transform: uppercase;
  margin-top: 0.125rem;
}

.footer__tagline {
  font-family: var(--font-serif);
  font-style: italic;
  font-size: 1.125rem;
  color: var(--color-text-muted);
  line-height: 1.5;
}

.footer__heading {
  font-family: var(--font-sans);
  font-size: 0.6875rem;
  font-weight: 500;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-text-dim);
  margin-bottom: 1.25rem;
}

.footer__nav ul,
.footer__contact ul,
.footer__legal ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  font-size: 0.9375rem;
  color: var(--color-text-muted);
}

.footer__nav a:hover {
  color: var(--color-accent);
}

.footer__bottom {
  border-top: 1px solid var(--color-line);
  padding: 1.5rem 0;
}

.footer__bottom-inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 0.8125rem;
  color: var(--color-text-dim);
  gap: 1rem;
  flex-wrap: wrap;
}

.footer__made {
  font-style: italic;
  font-family: var(--font-serif);
}

@media (max-width: 900px) {
  .footer__inner {
    grid-template-columns: 1fr 1fr;
  }

  .footer__brand {
    grid-column: span 2;
  }
}

@media (max-width: 500px) {
  .footer__inner {
    grid-template-columns: 1fr;
  }

  .footer__brand {
    grid-column: span 1;
  }

  .footer__bottom-inner {
    flex-direction: column;
    text-align: center;
  }
}
</style>