<script setup>
const props = defineProps({
  favorites: Array
})

const emit = defineEmits(['toggle-favorite'])

const formatPrice = (price) => {
  return new Intl.NumberFormat('ru-RU', {
    style: 'currency',
    currency: 'RUB',
    maximumFractionDigits: 0
  }).format(price)
}
</script>

<template>
  <section class="favorites">
    <h2>❤️ Избранное</h2>

    <div v-if="!favorites.length" class="empty">
      Нет избранных товаров
    </div>

    <div v-else class="grid">
      <div v-for="item in favorites" :key="item.id" class="card">
        
        <img :src="item.image" :alt="item.title" />

        <div class="info">
          <h3>{{ item.title }}</h3>
          <p class="price">{{ formatPrice(item.price) }}</p>

          <button @click="emit('toggle-favorite', item)">
            Удалить ❤️
          </button>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
.favorites {
  padding: 40px 20px;
  color: white;
}

h2 {
  font-size: 32px;
  margin-bottom: 20px;
}

.empty {
  color: #aaa;
  font-size: 16px;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 20px;
}

.card {
  background: #151519;
  border: 1px solid rgba(215,181,109,0.2);
  border-radius: 12px;
  overflow: hidden;
  transition: 0.3s;
}

.card:hover {
  transform: translateY(-5px);
}

.card img {
  width: 100%;
  height: 180px;
  object-fit: cover;
}

.info {
  padding: 12px;
}

.price {
  color: #d7b56d;
  font-weight: bold;
}

button {
  margin-top: 10px;
  background: none;
  border: 1px solid #d7b56d;
  color: #d7b56d;
  padding: 6px 10px;
  cursor: pointer;
  border-radius: 6px;
}

button:hover {
  background: #d7b56d;
  color: black;
}
</style>