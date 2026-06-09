<script setup>
import { ref } from 'vue'
import WatchCard from './WatchCard.vue'

const emit = defineEmits(['add-to-cart'])

const watches = ref([
  {
    id: 1,
    title: 'Certina DS Action',
    description: 'Спортивные часы с надёжным корпусом из нержавеющей стали и механизмом Ronda Quartz. Водостойкость до 100м, идеальны для активного образа жизни.',
    price: 89900,
    image: 'https://ulan-ude.timebit.ru/upload/iblock/606/60636f9b38c2fc198d1509041b978db1.jpg'
  },
  {
    id: 2,
    title: 'Seiko Prospex',
    description: 'Классические часы с автоматическим механизмом и сапфировым стеклом. Корпус из полированной нержавеющей стали, водостойкость 200м. Элегантный дизайн для деловых встреч.',
    price: 124500,
    image: 'https://images.firstclasswatches.com/EC-ErCaQdydO4MO5fJ9zg5372YOf6HtH98i00VcFsgY/rs:fit:0:1000/bg:fffcfa/bG9jYWw6Ly8vaW1hZ2VzL3Byb2R1Y3RzL3Byb2R1Y3QxNjI3NDAtOTkxMl9jcm9wcGVkLnBuZw.jpg'
  },
  {
    id: 3,
    title: 'Tag Heuer Carrera',
    description: 'Хронограф с трехсчетчиком и функцией секундомера. Швейцарский механизм, корпус из титана, сапфировое стекло с антибликовым покрытием. Люминесцентные стрелки для видимости в темноте.',
    price: 156000,
    image: 'https://chrono.ru/netcat_files/multifile/202/4799/CV2010.BA0794.jpg'
  },
  {
    id: 4,
    title: 'Omega Seamaster',
    description: 'Восстановленная классика с механическим движением Cal. 1120. Корпус из розового золота 18K, вечный циферблат. Гарантия подлинности с сертификатом производителя.',
    price: 285000,
    image: 'https://chrono.ru/netcat_files/multifile/202/18779/210.30.42.20.01.001_.jpg'
  },
  {
    id: 5,
    title: 'Breitling Titanium Pro',
    description: 'Легкие и прочные часы из авиационного титана. Механизм хронограф с 12-часовой шкалой, водостойкость 300м. Идеальны для пилотов и экстремальных условий.',
    price: 187500,
    image: 'https://spb.kronostime.ru/upload/resize_cache/iblock/36b/v2mj67rpoqey2cqj881qvf6qcsqwo9e3/99999_446_1/E823106A1BDS1.jpg'
  },
  {
    id: 6,
    title: 'Rolex Day-Date',
    description: 'Роскошные часы с позолотой 18K и кожаным ремешком крокодила. День и дата на циферблате, механизм Perpetual, водостойкость 100м. Символ статуса и успеха.',
    price: 450000,
    image: 'https://www.swisschrono.ru/wa-data/public/shop/products/28/56/55628/images/80282/80282.970.png'
  },
  {
    id: 7,
    title: 'Tudor Black Bay',
    description: 'Дайверские часы с черным циферблатом и красной полоской на ободе. Механизм автоматический MT5602, корпус из нержавеющей стали, водостойкость 200м.',
    price: 198500,
    image: 'https://submarinashop.ru/assets/images/products/5557/large/79030n-tudor-black-bay-1.jpg'
  },
  {
    id: 8,
    title: 'IWC Pilot Watch',
    description: 'Часы пилота с эргономичным дизайном и крупными легко читаемыми цифрами. Швейцарский механизм, корпус из нержавеющей стали. Люминесцентные стрелки, водостойкость 60м.',
    price: 164000,
    image: 'https://www.swisschrono.ru/wa-data/public/shop/products/85/98/59885/images/93081/93081.970.jpg'
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
  transition: 0.3s;
}

.sort-controls select:hover {
  border-color: #d7b56d;
}

.sort-controls select:focus {
  outline: none;
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