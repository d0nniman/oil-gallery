<!-- src/components/AboutSection.vue -->
<template>
  <section id="about" class="about">
    <div class="container about__inner">
      <div class="about__visual reveal">
        <div class="about__image-wrap">
          <img 
            src="https://images.unsplash.com/photo-1460661419201-fd4cecdf8a8b?w=800&q=80" 
            alt="Мастерская художника"
            class="about__image"
            loading="lazy"
          />
        </div>
        <div class="about__signature">
          <span class="about__signature-mark">O.N.</span>
          <span class="about__signature-text">Olivia Noir</span>
        </div>
      </div>

      <div class="about__content">
        <span class="overline reveal">О художнике</span>
        <h2 class="about__title reveal">
          Нефть — это<br />
          <em>материал времени.</em>
        </h2>

        <div class="about__text reveal">
          <p>
            Я работаю с нефтью более двенадцати лет. Этот материал 
            требует терпения — каждый слой сохнет неделями, но именно 
            поэтому картины приобретают ту глубину, за которую их ценят 
            коллекционеры.
          </p>
          <p>
            Мои работы находятся в частных коллекциях в Москве, 
            Берлине, Лондоне и Нью-Йорке. Я не тиражирую картины — 
            каждая существует в единственном экземпляре.
          </p>
        </div>

        <dl class="about__stats reveal">
          <div class="stat">
            <dt class="stat__number">12+</dt>
            <dd class="stat__label">лет с материалом</dd>
          </div>
          <div class="stat">
            <dt class="stat__number">180</dt>
            <dd class="stat__label">авторских работ</dd>
          </div>
          <div class="stat">
            <dt class="stat__number">24</dt>
            <dd class="stat__label">персональные выставки</dd>
          </div>
        </dl>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  padding: clamp(4rem, 10vw, 8rem) 0;
  background: var(--color-bg-warm);
  position: relative;
  overflow: hidden;
}

.about::before {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  width: 40%;
  height: 100%;
  background: radial-gradient(ellipse at right, rgba(184, 147, 90, 0.04) 0%, transparent 70%);
  pointer-events: none;
}

.about__inner {
  display: grid;
  grid-template-columns: 1fr 1.1fr;
  gap: clamp(2rem, 6vw, 6rem);
  align-items: center;
  position: relative;
}

.about__visual {
  position: relative;
}

.about__image-wrap {
  aspect-ratio: 4 / 5;
  overflow: hidden;
  background: var(--color-bg);
  position: relative;
}

.about__image-wrap::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(180deg, transparent 60%, rgba(10, 10, 10, 0.4) 100%);
}

.about__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: saturate(0.85) contrast(1.05);
}

.about__signature {
  position: absolute;
  bottom: -1.5rem;
  right: -1.5rem;
  background: var(--color-bg);
  padding: 1.5rem 2rem;
  border: 1px solid var(--color-line);
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 0.25rem;
}

.about__signature-mark {
  font-family: var(--font-serif);
  font-size: 2rem;
  font-style: italic;
  color: var(--color-accent);
  line-height: 1;
}

.about__signature-text {
  font-size: 0.6875rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-text-muted);
}

.about__content {
  position: relative;
  z-index: 1;
}

.about__title {
  font-size: clamp(2.25rem, 4.5vw, 3.5rem);
  font-weight: 300;
  line-height: 1.1;
  margin: 1.5rem 0 2rem;
}

.about__title em {
  font-style: italic;
  color: var(--color-accent);
}

.about__text {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
  font-size: 1.0625rem;
  color: var(--color-text-muted);
  line-height: 1.75;
  max-width: 540px;
  margin-bottom: 3rem;
}

.about__stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  padding-top: 2rem;
  border-top: 1px solid var(--color-line);
}

.stat__number {
  font-family: var(--font-serif);
  font-size: clamp(2rem, 3.5vw, 3rem);
  font-weight: 400;
  color: var(--color-text);
  line-height: 1;
  margin-bottom: 0.5rem;
}

.stat__label {
  font-size: 0.8125rem;
  color: var(--color-text-muted);
  line-height: 1.4;
}

@media (max-width: 900px) {
  .about__inner {
    grid-template-columns: 1fr;
  }

  .about__signature {
    right: 1rem;
    bottom: -1rem;
    padding: 1rem 1.5rem;
  }

  .about__signature-mark {
    font-size: 1.5rem;
  }

  .about__stats {
    gap: 1rem;
  }
}

@media (max-width: 500px) {
  .about__stats {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .stat {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    padding-bottom: 1.5rem;
    border-bottom: 1px solid var(--color-line);
  }

  .stat:last-child {
    padding-bottom: 0;
    border-bottom: none;
  }

  .stat__number {
    margin-bottom: 0;
  }
}
</style>