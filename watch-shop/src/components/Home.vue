<script setup>
defineEmits(['navigate'])
</script>

<template>
  <section class="home">
    <div class="hero">
      <div class="hero-content">
        <h1>Элегантность на вашем запястье</h1>
        <p>Премиум часы от ведущих мировых производителей</p>
        <button @click="$emit('navigate', 'catalog')" class="cta-btn">
          Смотреть каталог
        </button>
      </div>
      <div class="hero-image">🕦</div>
    </div>

    <section class="features">
      <div class="feature">
        <div class="feature-icon">✓</div>
        <h3>Оригинальность</h3>
        <p>Только оригинальные часы от авторизованных дилеров</p>
      </div>
      <div class="feature">
        <div class="feature-icon">🚚</div>
        <h3>Доставка</h3>
        <p>Быстрая доставка по всей России за 1-3 дня</p>
      </div>
      <div class="feature">
        <div class="feature-icon">🛡️</div>
        <h3>Гарантия</h3>
        <p>2 года гарантии на все часы и бесплатное обслуживание</p>
      </div>
    </section>
  </section>
</template>

<style scoped>
.home {
  color: white;
  padding: 40px 20px 60px;
}

.hero {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 60px;
  margin-bottom: 80px;
  padding: 40px 20px;
  background: linear-gradient(135deg, rgba(215, 181, 109, 0.1) 0%, transparent 100%);
  border-radius: 16px;
  border: 1px solid rgba(215, 181, 109, 0.2);
}

.hero-content h1 {
  margin: 0 0 16px;
  font-size: 48px;
  font-weight: 900;
  color: #d7b56d;
}

.hero-content p {
  margin: 0 0 32px;
  font-size: 18px;
  color: #bfbfbf;
  line-height: 1.6;
}

.cta-btn {
  padding: 14px 32px;
  background: #d7b56d;
  color: black;
  border: none;
  border-radius: 8px;
  font-weight: 700;
  font-size: 16px;
  cursor: pointer;
  transition: 0.3s;
}

.cta-btn:hover {
  background: #e5c578;
  transform: translateY(-2px);
}

.hero-image {
  font-size: 120px;
  opacity: 0.8;
}

.features {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
  margin-top: 60px;
}

.feature {
  background: rgba(215, 181, 109, 0.08);
  border: 1px solid rgba(215, 181, 109, 0.15);
  border-radius: 12px;
  padding: 30px 20px;
  text-align: center;
  transition: 0.3s;
}

.feature:hover {
  border-color: rgba(215, 181, 109, 0.4);
  background: rgba(215, 181, 109, 0.12);
}

.feature-icon {
  font-size: 40px;
  margin-bottom: 16px;
}

.feature h3 {
  margin: 0 0 12px;
  font-size: 20px;
}

.feature p {
  color: #bfbfbf;
  font-size: 14px;
  line-height: 1.6;
}

@media (max-width: 900px) {
  .hero {
    flex-direction: column;
    gap: 30px;
  }

  .hero-content h1 {
    font-size: 36px;
  }

  .hero-image {
    font-size: 80px;
  }

  .features {
    grid-template-columns: 1fr;
  }
}
</style>