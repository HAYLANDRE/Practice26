<script setup>
import { ref } from 'vue'
import WatchCard from './WatchCard.vue'

const emit = defineEmits(['add-to-cart'])

const watches = ref([
  {
    id: 1,
    title: 'Certina DS Action',
    description: 'Спортивные часы с надёжным корпусом и строгим дизайном.',
    price: 89900,
    image: 'https://images.unsplash.com/photo-1524592094714-0f0654e20314?q=80&w=900&auto=format&fit=crop'
  },
  {
    id: 2,
    title: 'Classic Automatic',
    description: 'Классическая модель для делового образа.',
    price: 124500,
    image: 'https://images.unsplash.com/photo-1508685096489-7aacd43bd3b1?q=80&w=900&auto=format&fit=crop'
  },
  {
    id: 3,
    title: 'Sport Chronograph',
    description: 'Хронограф с выразительным циферблатом.',
    price: 156000,
    image: 'https://images.unsplash.com/photo-1548171915-e79a380a2a4b?q=80&w=900&auto=format&fit=crop'
  },
  {
    id: 4,
    title: 'Vintage Heritage',
    description: 'Восстановленная классика на механизме ETA.',
    price: 95000,
    image: 'https://images.unsplash.com/photo-1523293182986-7651a695b37f?q=80&w=900&auto=format&fit=crop'
  },
  {
    id: 5,
    title: 'Titanium Pro',
    description: 'Легкие и прочные часы из титана для активного образа жизни.',
    price: 187500,
    image: 'https://images.unsplash.com/photo-1495856458515-0637185298c1?q=80&w=900&auto=format&fit=crop'
  },
  {
    id: 6,
    title: 'Gold Elegant',
    description: 'Роскошные часы с позолотой и кожаным ремешком.',
    price: 234000,
    image: 'https://images.unsplash.com/photo-1505778276668-fc4ee3ce4808?q=80&w=900&auto=format&fit=crop'
  }
])

const sortBy = ref('name')

const sortedWatches = computed(() => {
  let sorted = [...watches.value]
  if (sortBy.value === 'price-low') {
    sorted.sort((a, b) => a.price - b.price)
  } else if (sortBy.value === 'price-high') {
    sorted.sort((a, b) => b.price - a.price)
  }
  return sorted
})

import { computed } from 'vue'
</script>

<template>
  <section class="catalog">
    <div class="catalog-header">
      <h2>Каталог часов</h2>
      <div class="sort-controls">
        <label>Сортировка:</label>
        <select v-model="sortBy">
          <option value="name">По названию</option>
          <option value="price-low">Цена: от низкой</option>
          <option value="price-high">Цена: от высокой</option>
        </select>
      </div>
    </div>

    <div class="cards">
      <WatchCard
        v-for="watch in sortedWatches"
        :key="watch.id"
        :watch="watch"
        @add-to-cart="emit('add-to-cart', watch)"
      />
    </div>
  </section>
</template>

<style scoped>
.catalog {
  padding: 40px 20px 60px;
  color: white;
}

.catalog-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 32px;
  flex-wrap: wrap;
  gap: 20px;
}

.catalog-header h2 {
  margin: 0;
  font-size: 38px;
}

.sort-controls {
  display: flex;
  align-items: center;
  gap: 12px;
}

.sort-controls label {
  color: #bfbfbf;
  font-size: 14px;
}

.sort-controls select {
  background: #151519;
  border: 1px solid rgba(215, 181, 109, 0.3);
  color: white;
  padding: 8px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
}

.sort-controls select:hover {
  border-color: #d7b56d;
}

.cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 24px;
}

@media (max-width: 900px) {
  .catalog-header {
    flex-direction: column;
    align-items: flex-start;
  }

  .cards {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .cards {
    grid-template-columns: 1fr;
  }
}
</style>