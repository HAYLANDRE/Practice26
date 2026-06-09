<script setup>
const watches = [
  {
    id: 1,
    title: 'Certina DS Action',
    description: 'Спортивные часы с надёжным корпусом и строгим дизайном.',
    price: '89 900 ₽',
    image: 'https://images.unsplash.com/photo-1524592094714-0f0654e20314?q=80&w=900&auto=format&fit=crop'
  },
  {
    id: 2,
    title: 'Classic Automatic',
    description: 'Классическая модель для делового образа.',
    price: '124 500 ₽',
    image: 'https://images.unsplash.com/photo-1508685096489-7aacd43bd3b1?q=80&w=900&auto=format&fit=crop'
  },
  {
    id: 3,
    title: 'Sport Chronograph',
    description: 'Хронограф с выразительным циферблатом.',
    price: '156 000 ₽',
    image: 'https://images.unsplash.com/photo-1548171915-e79a380a2a4b?q=80&w=900&auto=format&fit=crop'
  }
]
</script>

<template>
  <section id="catalog" class="catalog">
    <h2>Каталог часов</h2>

    <div class="cards">
      <div class="card" v-for="watch in watches" :key="watch.id">
        <img :src="watch.image" :alt="watch.title">

        <div class="card-info">
          <h3>{{ watch.title }}</h3>
          <p>{{ watch.description }}</p>

          <div class="bottom">
            <span>{{ watch.price }}</span>
            <button>Подробнее</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.catalog {
  max-width: 1200px;
  margin: 0 auto;
  padding: 40px 30px 80px;
  color: white;
}

.catalog h2 {
  font-size: 38px;
  margin-bottom: 28px;
}

.cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 25px;
}

.card {
  background: #151519;
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 24px;
  overflow: hidden;
  transition: 0.3s;
}

.card:hover {
  transform: translateY(-8px);
  border-color: rgba(215,181,109,0.5);
}

.card img {
  width: 100%;
  height: 260px;
  object-fit: cover;
}

.card-info {
  padding: 22px;
}

.card h3 {
  margin: 0 0 10px;
  font-size: 22px;
}

.card p {
  color: #bfbfbf;
  line-height: 1.5;
}

.bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 20px;
}

.bottom span {
  color: #d7b56d;
  font-size: 20px;
  font-weight: 900;
}

.bottom button {
  border: none;
  padding: 10px 14px;
  border-radius: 12px;
  background: white;
  color: black;
  font-weight: 800;
  cursor: pointer;
}

.bottom button:hover {
  background: #d7b56d;
}

@media (max-width: 900px) {
  .cards {
    grid-template-columns: 1fr;
  }
}
</style>