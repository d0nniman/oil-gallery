<!-- src/components/HeroSection.vue -->
<template>
  <section id="home" class="hero">
    <div class="container hero__inner">
      <div class="hero__content">
        <div class="hero__meta reveal">
          <span class="overline">Est. 2012 · Москва</span>
        </div>
        
        <h1 class="hero__title reveal">
          <span class="hero__title-line">Картины,</span>
          <span class="hero__title-line hero__title-line--italic">рождённые</span>
          <span class="hero__title-line">из нефти.</span>
        </h1>

        <p class="hero__description reveal">
          Авторская галерея уникальных работ, выполненных в технике нефтяной живописи. 
          Каждая картина существует в единственном экземпляре — 
          глубокие текстуры, приглушённая палитра, вечные сюжеты.
        </p>

        <div class="hero__actions reveal">
          <a href="#collection" class="btn btn--primary">
            Смотреть коллекцию
            <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
              <path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" stroke-width="1.5"/>
            </svg>
          </a>
          <a href="#about" class="btn btn--ghost">Об авторе</a>
        </div>
      </div>

      <div class="hero__visual reveal">
        <div class="hero__frame">
          <img 
            src="https://images.unsplash.com/photo-1578926288207-a90a5366759d?w=800&q=80" 
            alt="Авторская картина нефтью"
            class="hero__image"
            loading="eager"
          />
          <div class="hero__frame-caption">
            <span>№ 01 / 12</span>
            <span>«Тихий вечер», 2024</span>
          </div>
        </div>
      </div>
    </div>

    <div class="hero__scroll reveal">
      <span class="hero__scroll-text">Прокрутите вниз</span>
      <span class="hero__scroll-line"></span>
    </div>
  </section>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  padding: 8rem 0 4rem;
  display: flex;
  flex-direction: column;
  position: relative;
  background: 
    radial-gradient(ellipse at top right, rgba(184, 147, 90, 0.08) 0%, transparent 50%),
    var(--color-bg);
}

.hero__inner {
  flex: 1;
  display: grid;
  grid-template-columns: 1.1fr 1fr;
  gap: clamp(2rem, 6vw, 6rem);
  align-items: center;
}

.hero__meta {
  margin-bottom: 2rem;
}

.hero__title {
  font-size: clamp(3rem, 7vw, 6rem);
  font-weight: 300;
  line-height: 1.05;
  letter-spacing: -0.02em;
  margin-bottom: 2rem;
}

.hero__title-line {
  display: block;
}

.hero__title-line--italic {
  font-style: italic;
  color: var(--color-accent);
  padding-left: clamp(1rem, 4vw, 3rem);
}

.hero__description {
  font-size: 1.0625rem;
  color: var(--color-text-muted);
  max-width: 480px;
  line-height: 1.7;
  margin-bottom: 3rem;
}

.hero__actions {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem 2rem;
  font-size: 0.875rem;
  font-weight: 500;
  letter-spacing: 0.05em;
  border-radius: 2px;
  transition: all var(--duration-normal) var(--ease-out);
  cursor: pointer;
}

.btn--primary {
  background: var(--color-text);
  color: var(--color-bg);
}

.btn--primary:hover {
  background: var(--color-accent);
  color: var(--color-bg);
}

.btn--primary svg {
  transition: transform var(--duration-normal) var(--ease-out);
}

.btn--primary:hover svg {
  transform: translateX(4px);
}

.btn--ghost {
  border: 1px solid var(--color-line-strong);
  color: var(--color-text);
}

.btn--ghost:hover {
  border-color: var(--color-text);
}

.hero__visual {
  position: relative;
}

.hero__frame {
  position: relative;
  aspect-ratio: 4 / 5;
  overflow: hidden;
  background: var(--color-bg-warm);
}

.hero__frame::before {
  content: '';
  position: absolute;
  inset: 1rem;
  border: 1px solid var(--color-accent-dim);
  pointer-events: none;
  z-index: 2;
}

.hero__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 1.2s var(--ease-out);
  filter: saturate(0.9) contrast(1.05);
}

.hero__frame:hover .hero__image {
  transform: scale(1.03);
}

.hero__frame-caption {
  position: absolute;
  bottom: 1.5rem;
  left: 1.5rem;
  right: 1.5rem;
  display: flex;
  justify-content: space-between;
  font-size: 0.75rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-text);
  z-index: 3;
  mix-blend-mode: difference;
}

.hero__scroll {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.75rem;
  margin-top: 4rem;
}

.hero__scroll-text {
  font-size: 0.6875rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-text-dim);
}

.hero__scroll-line {
  width: 1px;
  height: 40px;
  background: linear-gradient(to bottom, var(--color-accent), transparent);
  animation: scrollLine 2s var(--ease-in-out) infinite;
}

@keyframes scrollLine {
  0%, 100% { opacity: 0.3; transform: scaleY(0.5); }
  50% { opacity: 1; transform: scaleY(1); }
}

@media (max-width: 900px) {
  .hero {
    padding: 7rem 0 3rem;
    min-height: auto;
  }

  .hero__inner {
    grid-template-columns: 1fr;
    gap: 3rem;
  }

  .hero__title {
      font-size: clamp(3rem, 7vw, 6rem);
    font-size: clamp(3rem, 10vw, 5rem);
  }

  .hero__description {
    font-size: 1rem;
  }

  .hero__scroll {
    display: none;
  }
}
</style>