<script setup>
defineEmits(['navigate'])

const reviews = [
  {
    id: 1,
    name: 'Александр П.',
    rating: 5,
    text: 'Отличный сервис! Часы пришли быстро и в идеальном состоянии.',
    watch: 'Rolex Submariner'
  },
  {
    id: 2,
    name: 'Мария К.',
    rating: 5,
    text: 'Кольцо покупала мужу - он в восторге! Рекомендую.',
    watch: 'Omega Seamaster'
  },
  {
    id: 3,
    name: 'Иван С.',
    rating: 5,
    text: 'Профессиональная консультация, качественный товар.',
    watch: 'TAG Heuer Carrera'
  }
]

const topWatches = [
  { id: 1, name: 'Rolex Submariner', price: '580 000 ₽', icon: '⌚', color: '#d4af37' },
  { id: 2, name: 'Omega Seamaster', price: '450 000 ₽', icon: '🕐', color: '#c9b037' },
  { id: 3, name: 'TAG Heuer Carrera', price: '320 000 ₽', icon: '⏱️', color: '#daa520' }
]

const stats = [
  { value: '12K+', label: 'Довольных клиентов', icon: '😊' },
  { value: '500+', label: 'Часов в каталоге', icon: '⌚' },
  { value: '10 лет', label: 'На рынке', icon: '⏰' }
]
</script>

<template>
  <section class="home">
    <!-- Улучшенный Hero раздел -->
    <div class="hero">
      <div class="hero-glow"></div>
      <div class="hero-content">
        <div class="hero-badge">✨ Премиум коллекция 2024</div>
        <h1>Элегантность<br/>на вашем запястье</h1>
        <p>Откройте мир люксовых часов от ведущих мировых производителей. Каждый момент времени заслуживает стиля.</p>
        <div class="cta-group">
          <button @click="$emit('navigate', 'catalog')" class="cta-btn primary">
            Смотреть каталог
          </button>
          <button @click="$emit('navigate', 'about')" class="cta-btn secondary">
            Узнать больше
          </button>
        </div>
      </div>
      <div class="hero-image">
        <div class="watch-display">⌚</div>
        <div class="floating-elements">
          <span class="float-1">✨</span>
          <span class="float-2">💎</span>
          <span class="float-3">⭐</span>
        </div>
      </div>
    </div>

    <!-- Статистика -->
    <section class="stats-section">
      <div v-for="stat in stats" :key="stat.value" class="stat-card">
        <div class="stat-icon">{{ stat.icon }}</div>
        <div class="stat-value">{{ stat.value }}</div>
        <div class="stat-label">{{ stat.label }}</div>
      </div>
    </section>

    <!-- Популярные часы -->
    <section class="top-watches">
      <div class="section-header">
        <h2>Популярные модели</h2>
        <p>Самые желаемые часы нашей коллекции</p>
      </div>
      <div class="watches-grid">
        <div v-for="watch in topWatches" :key="watch.id" class="watch-card" :style="{ '--accent-color': watch.color }">
          <div class="watch-icon">{{ watch.icon }}</div>
          <h3>{{ watch.name }}</h3>
          <p class="watch-price">{{ watch.price }}</p>
          <button @click="$emit('navigate', 'catalog')" class="view-btn">Смотреть</button>
        </div>
      </div>
    </section>

    <!-- Преимущества -->
    <section class="features">
      <div class="section-header">
        <h2>Почему выбирают нас</h2>
        <p>Мы гарантируем лучший опыт покупки</p>
      </div>
      <div class="features-grid">
        <div class="feature">
          <div class="feature-icon">✓</div>
          <h3>100% Оригинальность</h3>
          <p>Только оригинальные часы от авторизованных дилеров. Каждый товар проходит проверку подлинности.</p>
        </div>
        <div class="feature">
          <div class="feature-icon">🚚</div>
          <h3>Быстрая доставка</h3>
          <p>Доставка по всей России за 1-3 дня. Упаковка со специальной защитой.</p>
        </div>
        <div class="feature">
          <div class="feature-icon">🛡️</div>
          <h3>Расширенная гарантия</h3>
          <p>2 года гарантии и бесплатное обслуживание. Консультации специалистов.</p>
        </div>
        <div class="feature">
          <div class="feature-icon">💳</div>
          <h3>Удобная оплата</h3>
          <p>Все способы оплаты. Рассрочка до 12 месяцев без процентов.</p>
        </div>
        <div class="feature">
          <div class="feature-icon">🤝</div>
          <h3>Личный консультант</h3>
          <p>Поможем выбрать идеальные часы под ваш стиль и бюджет.</p>
        </div>
        <div class="feature">
          <div class="feature-icon">⭐</div>
          <h3>Эксклюзивные предложения</h3>
          <p>VIP-программа для постоянных клиентов с персональными скидками.</p>
        </div>
      </div>
    </section>

    <!-- Отзывы -->
    <section class="reviews-section">
      <div class="section-header">
        <h2>Отзывы наших клиентов</h2>
        <p>Доверие клиентов - наша главная ценность</p>
      </div>
      <div class="reviews-grid">
        <div v-for="review in reviews" :key="review.id" class="review-card">
          <div class="review-stars">
            <span v-for="i in 5" :key="i" class="star">⭐</span>
          </div>
          <p class="review-text">{{ review.text }}</p>
          <div class="review-author">
            <strong>{{ review.name }}</strong>
            <span class="review-watch">{{ review.watch }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Newsletter -->
    <section class="newsletter">
      <div class="newsletter-content">
        <h2>Не пропустите эксклюзивные предложения</h2>
        <p>Подпишитесь на нашу рассылку и получите скидку 10% на первую покупку</p>
        <div class="newsletter-form">
          <input type="email" placeholder="Введите ваш email" class="newsletter-input">
          <button class="newsletter-btn">Подписаться</button>
        </div>
      </div>
    </section>
  </section>
</template>

<style scoped>
.home {
  color: white;
  padding: 0;
}

/* Hero Section */
.hero {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 60px;
  padding: 80px 40px;
  background: linear-gradient(135deg, rgba(215, 181, 109, 0.15) 0%, rgba(215, 181, 109, 0.05) 50%, transparent 100%);
  border-bottom: 1px solid rgba(215, 181, 109, 0.15);
  overflow: hidden;
  min-height: 600px;
}

.hero-glow {
  position: absolute;
  top: -50%;
  right: -20%;
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, rgba(215, 181, 109, 0.1) 0%, transparent 70%);
  border-radius: 50%;
  filter: blur(40px);
  pointer-events: none;
}

.hero-content {
  flex: 1;
  z-index: 1;
  animation: slideIn 0.8s ease-out;
}

.hero-badge {
  display: inline-block;
  padding: 8px 16px;
  background: rgba(215, 181, 109, 0.15);
  border: 1px solid rgba(215, 181, 109, 0.3);
  border-radius: 24px;
  font-size: 13px;
  color: #d7b56d;
  margin-bottom: 24px;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 600;
}

.hero-content h1 {
  margin: 0 0 24px;
  font-size: 64px;
  font-weight: 900;
  color: white;
  line-height: 1.2;
  background: linear-gradient(135deg, #d7b56d 0%, #e5c578 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-content p {
  margin: 0 0 40px;
  font-size: 18px;
  color: #bfbfbf;
  line-height: 1.8;
  max-width: 500px;
}

.cta-group {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}

.cta-btn {
  padding: 16px 36px;
  border: none;
  border-radius: 10px;
  font-weight: 700;
  font-size: 16px;
  cursor: pointer;
  transition: 0.3s;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.cta-btn.primary {
  background: #d7b56d;
  color: black;
}

.cta-btn.primary:hover {
  background: #e5c578;
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(215, 181, 109, 0.2);
}

.cta-btn.secondary {
  background: transparent;
  color: #d7b56d;
  border: 2px solid #d7b56d;
}

.cta-btn.secondary:hover {
  background: rgba(215, 181, 109, 0.1);
  transform: translateY(-2px);
}

.hero-image {
  flex: 1;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1;
}

.watch-display {
  font-size: 200px;
  animation: float 3s ease-in-out infinite;
}

.floating-elements {
  position: absolute;
  width: 100%;
  height: 100%;
}

.float-1, .float-2, .float-3 {
  position: absolute;
  font-size: 48px;
  animation: float 4s ease-in-out infinite;
}

.float-1 { top: 20%; right: 20%; animation-delay: 0s; }
.float-2 { top: 60%; left: 10%; animation-delay: 1s; }
.float-3 { bottom: 20%; right: 30%; animation-delay: 2s; }

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-30px); }
}

/* Stats Section */
.stats-section {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
  padding: 60px 40px;
  background: rgba(215, 181, 109, 0.05);
  border-bottom: 1px solid rgba(215, 181, 109, 0.1);
}

.stat-card {
  text-align: center;
  padding: 30px;
  background: rgba(215, 181, 109, 0.08);
  border: 1px solid rgba(215, 181, 109, 0.15);
  border-radius: 12px;
  transition: 0.3s;
}

.stat-card:hover {
  background: rgba(215, 181, 109, 0.12);
  border-color: rgba(215, 181, 109, 0.3);
  transform: translateY(-4px);
}

.stat-icon {
  font-size: 48px;
  margin-bottom: 12px;
}

.stat-value {
  font-size: 36px;
  font-weight: 900;
  color: #d7b56d;
  margin-bottom: 8px;
}

.stat-label {
  font-size: 14px;
  color: #bfbfbf;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Top Watches Section */
.top-watches {
  padding: 80px 40px;
  border-bottom: 1px solid rgba(215, 181, 109, 0.1);
}

.section-header {
  text-align: center;
  margin-bottom: 50px;
}

.section-header h2 {
  font-size: 44px;
  margin-bottom: 12px;
  background: linear-gradient(135deg, #d7b56d 0%, #e5c578 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-header p {
  font-size: 16px;
  color: #bfbfbf;
}

.watches-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
}

.watch-card {
  background: linear-gradient(135deg, rgba(215, 181, 109, 0.1) 0%, transparent 100%);
  border: 1px solid rgba(215, 181, 109, 0.2);
  border-radius: 16px;
  padding: 40px 24px;
  text-align: center;
  transition: 0.3s;
  position: relative;
  overflow: hidden;
}

.watch-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: var(--accent-color);
}

.watch-card:hover {
  border-color: var(--accent-color);
  background: linear-gradient(135deg, rgba(215, 181, 109, 0.15) 0%, rgba(215, 181, 109, 0.05) 100%);
  transform: translateY(-8px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}

.watch-icon {
  font-size: 80px;
  margin-bottom: 16px;
  animation: float 3s ease-in-out infinite;
}

.watch-card h3 {
  font-size: 20px;
  margin-bottom: 12px;
  color: white;
}

.watch-price {
  font-size: 22px;
  font-weight: 700;
  color: var(--accent-color);
  margin-bottom: 20px;
}

.view-btn {
  padding: 10px 24px;
  background: var(--accent-color);
  color: black;
  border: none;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  transition: 0.3s;
}

.view-btn:hover {
  background: #fff;
  transform: scale(1.05);
}

/* Features Section */
.features {
  padding: 80px 40px;
  background: rgba(215, 181, 109, 0.03);
  border-bottom: 1px solid rgba(215, 181, 109, 0.1);
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
}

.feature {
  background: rgba(215, 181, 109, 0.08);
  border: 1px solid rgba(215, 181, 109, 0.15);
  border-radius: 12px;
  padding: 32px 24px;
  text-align: center;
  transition: 0.3s;
}

.feature:hover {
  border-color: rgba(215, 181, 109, 0.4);
  background: rgba(215, 181, 109, 0.12);
  transform: translateY(-6px);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
}

.feature-icon {
  font-size: 48px;
  margin-bottom: 16px;
  display: inline-block;
  transition: 0.3s;
}

.feature:hover .feature-icon {
  transform: scale(1.2);
}

.feature h3 {
  font-size: 18px;
  margin-bottom: 12px;
  color: #d7b56d;
}

.feature p {
  color: #bfbfbf;
  font-size: 14px;
  line-height: 1.6;
}

/* Reviews Section */
.reviews-section {
  padding: 80px 40px;
  border-bottom: 1px solid rgba(215, 181, 109, 0.1);
}

.reviews-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
}

.review-card {
  background: rgba(215, 181, 109, 0.08);
  border: 1px solid rgba(215, 181, 109, 0.15);
  border-radius: 12px;
  padding: 30px;
  transition: 0.3s;
}

.review-card:hover {
  background: rgba(215, 181, 109, 0.12);
  border-color: rgba(215, 181, 109, 0.3);
  transform: translateY(-4px);
}

.review-stars {
  display: flex;
  gap: 4px;
  margin-bottom: 16px;
}

.star {
  font-size: 16px;
}

.review-text {
  font-size: 14px;
  color: #bfbfbf;
  line-height: 1.6;
  margin-bottom: 20px;
  font-style: italic;
}

.review-author {
  display: flex;
  flex-direction: column;
  gap: 4px;
  padding-top: 16px;
  border-top: 1px solid rgba(215, 181, 109, 0.15);
}

.review-author strong {
  color: white;
  font-size: 14px;
}

.review-watch {
  font-size: 12px;
  color: #d7b56d;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Newsletter Section */
.newsletter {
  padding: 80px 40px;
  background: linear-gradient(135deg, rgba(215, 181, 109, 0.15) 0%, rgba(215, 181, 109, 0.05) 100%);
  border-bottom: 1px solid rgba(215, 181, 109, 0.15);
}

.newsletter-content {
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
}

.newsletter-content h2 {
  font-size: 36px;
  margin-bottom: 16px;
  background: linear-gradient(135deg, #d7b56d 0%, #e5c578 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.newsletter-content p {
  font-size: 16px;
  color: #bfbfbf;
  margin-bottom: 30px;
}

.newsletter-form {
  display: flex;
  gap: 12px;
}

.newsletter-input {
  flex: 1;
  padding: 14px 20px;
  background: rgba(0, 0, 0, 0.3);
  border: 1px solid rgba(215, 181, 109, 0.3);
  border-radius: 8px;
  color: white;
  font-size: 14px;
}

.newsletter-input::placeholder {
  color: #666;
}

.newsletter-input:focus {
  outline: none;
  border-color: #d7b56d;
  box-shadow: 0 0 0 2px rgba(215, 181, 109, 0.1);
}

.newsletter-btn {
  padding: 14px 32px;
  background: #d7b56d;
  color: black;
  border: none;
  border-radius: 8px;
  font-weight: 700;
  cursor: pointer;
  transition: 0.3s;
  white-space: nowrap;
}

.newsletter-btn:hover {
  background: #e5c578;
  transform: translateY(-2px);
}

/* Responsive */
@media (max-width: 900px) {
  .hero {
    flex-direction: column;
    gap: 40px;
    padding: 60px 20px;
    min-height: auto;
  }

  .hero-content h1 {
    font-size: 44px;
  }

  .watch-display {
    font-size: 120px;
  }

  .stats-section,
  .watches-grid,
  .features-grid,
  .reviews-grid {
    grid-template-columns: 1fr;
  }

  .hero-badge,
  .top-watches,
  .features,
  .reviews-section,
  .newsletter {
    padding: 40px 20px;
  }

  .section-header h2 {
    font-size: 32px;
  }

  .cta-group {
    flex-direction: column;
  }

  .newsletter-form {
    flex-direction: column;
  }

  .newsletter-btn {
    width: 100%;
  }
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateX(-30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}
</style>