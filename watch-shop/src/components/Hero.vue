<template>
  <section class="hero">
    <div class="hero-text">
      <p class="label">Премиальные часы</p>

      <h1>Точность. Стиль. Характер.</h1>

      <p class="description">
        Коллекция часов для тех, кто ценит качество, статус и современный дизайн.
      </p>

      <a href="#catalog" class="btn">
        Смотреть каталог
      </a>
    </div>

    <div class="hero-card">
      <img
        src="https://images.unsplash.com/photo-1523170335258-f5ed11844a49?q=80&w=900&auto=format&fit=crop"
        alt="watch"
      >
    </div>
  </section>
</template>

<style scoped>
.hero {
  max-width: 1200px;
  margin: 0 auto;
  padding: 80px 30px;
  display: grid;
  grid-template-columns: 1fr 480px;
  gap: 50px;
  align-items: center;
  color: white;
}

.label {
  color: #d7b56d;
  text-transform: uppercase;
  letter-spacing: 3px;
  font-size: 14px;
  font-weight: 800;
}

.hero h1 {
  font-size: 64px;
  line-height: 1.05;
  margin: 12px 0 20px;
}

.description {
  color: #c7c7c7;
  font-size: 20px;
  line-height: 1.6;
  max-width: 560px;
}

.btn {
  display: inline-block;
  margin-top: 25px;
  padding: 15px 24px;
  border-radius: 14px;
  background: linear-gradient(135deg, #d7b56d, #9d7430);
  color: black;
  text-decoration: none;
  font-weight: 900;
}

.hero-card {
  padding: 18px;
  border-radius: 28px;
  background: rgba(255, 255, 255, 0.08);
  box-shadow: 0 30px 80px rgba(0, 0, 0, 0.45);
}

.hero-card img {
  width: 100%;
  height: 520px;
  object-fit: cover;
  border-radius: 22px;
}

@media (max-width: 900px) {
  .hero {
    grid-template-columns: 1fr;
  }

  .hero h1 {
    font-size: 42px;
  }

  .hero-card img {
    height: 360px;
  }
}
</style>