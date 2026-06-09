<template>
  <section class="about">
    <h2>О компании</h2>

    <div class="about-grid">
      <div class="about-item">
        <h3>История</h3>
        <p>
          LUX WATCH основана в 2010 году как специализированный магазин премиум часов.
          За более чем десять лет мы завоевали репутацию надежного поставщика оригинальных
          часов от ведущих мировых брендов.
        </p>
      </div>

      <div class="about-item">
        <h3>Миссия</h3>
        <p>
          Мы стремимся сделать премиум часы доступными для каждого ценителя качества.
          Наша миссия - предоставлять только оригинальную продукцию с полной гарантией
          и профессиональным сервисом.
        </p>
      </div>

      <div class="about-item">
        <h3>Качество</h3>
        <p>
          Каждые часы в нашем каталоге проходят тщательную проверку подлинности.
          Мы работаем только с авторизованными дилерами и гарантируем качество
          каждого товара с момента покупки.
        </p>
      </div>

      <div class="about-item">
        <h3>Сервис</h3>
        <p>
          Наша команда профессионалов готова помочь вам выбрать идеальные часы.
          Мы предлагаем консультации, техническое обслуживание и ремонт всех моделей
          в нашем магазине.
        </p>
      </div>
    </div>

    <div class="stats">
      <div class="stat">
        <div class="stat-number">15+</div>
        <div class="stat-label">Лет опыта</div>
      </div>
      <div class="stat">
        <div class="stat-number">5000+</div>
        <div class="stat-label">Довольных клиентов</div>
      </div>
      <div class="stat">
        <div class="stat-number">200+</div>
        <div class="stat-label">Моделей в каталоге</div>
      </div>
      <div class="stat">
        <div class="stat-number">24/7</div>
        <div class="stat-label">Служба поддержки</div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  padding: 60px 20px;
  color: white;
}

.about h2 {
  margin: 0 0 40px;
  font-size: 38px;
  text-align: center;
}

.about-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 32px;
  margin-bottom: 60px;
}

.about-item {
  background: rgba(215, 181, 109, 0.08);
  border: 1px solid rgba(215, 181, 109, 0.15);
  border-radius: 12px;
  padding: 28px;
}

.about-item h3 {
  margin: 0 0 16px;
  font-size: 22px;
  color: #d7b56d;
}

.about-item p {
  margin: 0;
  color: #bfbfbf;
  line-height: 1.8;
}

.stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  margin-top: 40px;
}

.stat {
  text-align: center;
  padding: 30px 20px;
  background: rgba(215, 181, 109, 0.12);
  border: 1px solid rgba(215, 181, 109, 0.2);
  border-radius: 12px;
  transition: 0.3s;
}

.stat:hover {
  border-color: rgba(215, 181, 109, 0.4);
  background: rgba(215, 181, 109, 0.15);
}

.stat-number {
  font-size: 36px;
  font-weight: 900;
  color: #d7b56d;
  margin-bottom: 8px;
}

.stat-label {
  font-size: 14px;
  color: #bfbfbf;
}

@media (max-width: 900px) {
  .about-grid {
    grid-template-columns: 1fr;
  }

  .stats {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .stats {
    grid-template-columns: 1fr;
  }

  .about h2 {
    font-size: 28px;
  }
}
</style>