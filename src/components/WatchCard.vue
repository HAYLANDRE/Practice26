<template>
  <div class="card">
    <div class="card-image">
  <img :src="watch.image" :alt="watch.title">

  <div class="price-label">
    {{ formatPrice(watch.price) }}
  </div>

  <button
    class="favorite-btn"
    @click="toggleFavorite"
  >
    {{ isFavorite ? '❤️' : '🤍' }}
  </button>
</div>

    <div class="card-info">
      <h3>{{ watch.title }}</h3>
      <p>{{ watch.description }}</p>

      <button @click="$emit('add-to-cart')" class="add-btn">
        Добавить в корзину
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const props = defineProps({
  watch: Object
})

defineEmits(['add-to-cart'])

const isFavorite = ref(false)

onMounted(() => {
  const favorites =
    JSON.parse(localStorage.getItem('favorites')) || []

  isFavorite.value = favorites.some(
    item => item.title === props.watch.title
  )
})

const toggleFavorite = () => {
  let favorites =
    JSON.parse(localStorage.getItem('favorites')) || []

  const exists = favorites.find(
    item => item.title === props.watch.title
  )

  if (exists) {
    favorites = favorites.filter(
      item => item.title !== props.watch.title
    )
    isFavorite.value = false
  } else {
    favorites.push(props.watch)
    isFavorite.value = true
  }

  localStorage.setItem(
    'favorites',
    JSON.stringify(favorites)
  )
}

const formatPrice = (price) => {
  return new Intl.NumberFormat('ru-RU', {
    style: 'currency',
    currency: 'RUB',
    minimumFractionDigits: 0
  }).format(price)
}
</script>

<style scoped>
.card {
  background: #151519;
  border: 1px solid rgba(215, 181, 109, 0.15);
  border-radius: 12px;
  overflow: hidden;
  transition: 0.3s;
  display: flex;
  flex-direction: column;
  height: 100%;
}

.card:hover {
  transform: translateY(-6px);
  border-color: rgba(215, 181, 109, 0.5);
  box-shadow: 0 10px 30px rgba(215, 181, 109, 0.1);
}

.card-image {
  position: relative;
  overflow: hidden;
  height: 240px;
}

.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: 0.3s;
}

.card:hover .card-image img {
  transform: scale(1.08);
}

.price-label {
  position: absolute;
  top: 12px;
  right: 12px;
  background: #d7b56d;
  color: black;
  padding: 6px 12px;
  border-radius: 6px;
  font-weight: 700;
  font-size: 14px;
}

.card-info {
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  flex: 1;
}

.card-info h3 {
  margin: 0;
  font-size: 20px;
  color: white;
}

.card-info p {
  margin: 0;
  color: #bfbfbf;
  font-size: 14px;
  line-height: 1.5;
  flex: 1;
}

.add-btn {
  margin-top: auto;
  padding: 10px 16px;
  background: #d7b56d;
  color: black;
  border: none;
  border-radius: 8px;
  font-weight: 700;
  cursor: pointer;
  transition: 0.3s;
  font-size: 14px;
}

.add-btn:hover {
  background: #e5c578;
}

.add-btn:active {
  transform: scale(0.98);
}

.favorite-btn {
  position: absolute;
  top: 12px;
  left: 12px;

  width: 42px;
  height: 42px;

  border: none;
  border-radius: 50%;

  cursor: pointer;

  background: rgba(0,0,0,0.6);
  font-size: 20px;

  transition: 0.3s;
}

.favorite-btn:hover {
  transform: scale(1.1);
}
</style>