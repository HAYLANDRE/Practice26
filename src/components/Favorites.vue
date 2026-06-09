<script setup>
defineProps({
  favorites: Array
})

const emit = defineEmits(['toggle-favorite'])
</script>

<template>
  <div class="favorites">
    <h2>Избранные товары ❤️</h2>

    <div v-if="!favorites.length">
      Нет избранных товаров
    </div>

    <div v-for="item in favorites" :key="item.id">
      <p>{{ item.name }} - {{ item.price }} ₽</p>
      <button @click="emit('toggle-favorite', item)">
        Удалить ❤️
      </button>
    </div>
  </div>
</template>