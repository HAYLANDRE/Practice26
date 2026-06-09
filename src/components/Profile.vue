<script setup>
import { ref } from 'vue'

const props = defineProps({
  user: Object,
  orders: Array
})

const emit = defineEmits(['update-user'])

const address = ref(props.user?.address || '')

function saveAddress() {
  emit('update-user', {
    ...props.user,
    address: address.value
  })
}
</script>

<template>
  <section class="profile">
    <h2>Личный кабинет</h2>

    <div class="profile-card">
      <h3>Данные пользователя</h3>

      <p><b>Имя:</b> {{ user.name }}</p>
      <p><b>Email:</b> {{ user.email }}</p>
      <p><b>Телефон:</b> {{ user.phone }}</p>

      <div class="address-block">
        <label>Адрес доставки</label>
        <input
          v-model="address"
          type="text"
          placeholder="Введите адрес"
        >

        <button @click="saveAddress">
          Сохранить адрес
        </button>
      </div>
    </div>

    <div class="profile-card">
      <h3>История покупок</h3>

      <div v-if="orders.length === 0" class="empty">
        Покупок пока нет
      </div>

      <div
        v-for="order in orders"
        :key="order.id"
        class="order"
      >
        <p><b>Заказ №:</b> {{ order.id }}</p>
        <p><b>Дата:</b> {{ order.date }}</p>
        <p><b>Адрес:</b> {{ order.address }}</p>
        <p><b>Сумма:</b> {{ order.total }} ₽</p>

        <ul>
          <li v-for="item in order.items" :key="item.id">
            {{ item.title }} — {{ item.quantity }} шт.
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<style scoped>
.profile {
  max-width: 1000px;
  margin: 50px auto;
  padding: 0 30px;
  color: white;
}

.profile h2 {
  font-size: 38px;
  margin-bottom: 25px;
}

.profile-card {
  background: #151519;
  border: 1px solid rgba(215, 181, 109, 0.25);
  border-radius: 24px;
  padding: 28px;
  margin-bottom: 25px;
  box-shadow: 0 20px 45px rgba(0, 0, 0, 0.25);
}

.profile-card h3 {
  margin-top: 0;
  color: #d7b56d;
}

.address-block {
  margin-top: 20px;
}

.address-block label {
  display: block;
  margin-bottom: 8px;
  font-weight: 700;
}

input {
  width: 100%;
  box-sizing: border-box;
  padding: 13px;
  border-radius: 12px;
  border: 1px solid #444;
  background: #0b0b0d;
  color: white;
  margin-bottom: 12px;
}

button {
  padding: 12px 18px;
  border: none;
  border-radius: 12px;
  background: #d7b56d;
  color: black;
  font-weight: 800;
  cursor: pointer;
}

.order {
  background: #0f0f12;
  border-radius: 16px;
  padding: 18px;
  margin-bottom: 15px;
}

.empty {
  color: #aaa;
}
</style>