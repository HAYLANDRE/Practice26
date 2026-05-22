<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  cart: Array,
  user: Object
})

const emit = defineEmits(['remove', 'update-quantity', 'show-register'])

const showOrderModal = ref(false)
const orderData = ref({
  deliveryAddress: '',
  deliveryDate: ''
})

const total = computed(() => {
  return props.cart.reduce((sum, item) => sum + (item.price * item.quantity), 0)
})

const handleOrder = () => {
  if (!props.user) {
    emit('show-register')
    return
  }
  showOrderModal.value = true
}

const completeOrder = () => {
  showOrderModal.value = false
  orderData.value = { deliveryAddress: '', deliveryDate: '' }
  alert(`Заказ успешно оформлен!

Клиент: ${props.user.name}
Email: ${props.user.email}
Адрес доставки: ${orderData.value.deliveryAddress}
Дата доставки: ${orderData.value.deliveryDate}

Сумма: ${formatPrice(total.value)}

Спасибо за покупку!`)
}

const formatPrice = (price) => {
  return new Intl.NumberFormat('ru-RU', {
    style: 'currency',
    currency: 'RUB',
    minimumFractionDigits: 0
  }).format(price)
}
</script>

<template>
  <section class="cart">
    <h2>Корзина</h2>

    <div v-if="cart.length === 0" class="empty-cart">
      <div class="empty-icon">🛒</div>
      <p>Ваша корзина пуста</p>
    </div>

    <div v-else class="cart-content">
      <div class="cart-items">
        <div v-for="item in cart" :key="item.id" class="cart-item">
          <img :src="item.image" :alt="item.title" class="item-image">

          <div class="item-info">
            <h4>{{ item.title }}</h4>
            <p>{{ formatPrice(item.price) }} за шт.</p>
          </div>

          <div class="item-controls">
            <button @click="emit('update-quantity', item.id, item.quantity - 1)">−</button>
            <input
              type="number"
              v-model.number="item.quantity"
              @change="emit('update-quantity', item.id, item.quantity)"
              min="1"
            >
            <button @click="emit('update-quantity', item.id, item.quantity + 1)">+</button>
          </div>

          <div class="item-total">
            {{ formatPrice(item.price * item.quantity) }}
          </div>

          <button @click="emit('remove', item.id)" class="remove-btn">✕</button>
        </div>
      </div>

      <div class="cart-summary">
        <h3>Сумма заказа</h3>
        <div class="summary-row">
          <span>Товары:</span>
          <span>{{ formatPrice(total) }}</span>
        </div>
        <div class="summary-row">
          <span>Доставка:</span>
          <span>Бесплатно</span>
        </div>
        <div class="summary-total">
          <span>Итого:</span>
          <span>{{ formatPrice(total) }}</span>
        </div>

        <button @click="handleOrder" class="order-btn">
          Оформить заказ
        </button>
      </div>
    </div>

    <!-- Order Modal -->
    <div v-if="showOrderModal" class="modal-overlay" @click="showOrderModal = false">
      <div class="modal" @click.stop>
        <button class="close-btn" @click="showOrderModal = false">✕</button>
        <h3>Оформление заказа</h3>

        <div class="user-info">
          <p><strong>Клиент:</strong> {{ user.name }}</p>
          <p><strong>Email:</strong> {{ user.email }}</p>
          <p><strong>Телефон:</strong> {{ user.phone }}</p>
        </div>

        <form @submit.prevent="completeOrder">
          <label>Адрес доставки:</label>
          <input
            v-model="orderData.deliveryAddress"
            type="text"
            placeholder="Введите адрес доставки"
            required
          >

          <label>Предпочтительная дата доставки:</label>
          <input
            v-model="orderData.deliveryDate"
            type="date"
            required
          >

          <div class="order-total">
            <span>Сумма к оплате:</span>
            <span>{{ formatPrice(total) }}</span>
          </div>

          <button type="submit" class="submit-btn">Подтвердить заказ</button>
        </form>
      </div>
    </div>
  </section>
</template>

<style scoped>
.cart {
  padding: 60px 20px;
  color: white;
}

.cart h2 {
  margin: 0 0 40px;
  font-size: 38px;
}

.empty-cart {
  text-align: center;
  padding: 80px 20px;
}

.empty-icon {
  font-size: 80px;
  margin-bottom: 16px;
  opacity: 0.5;
}

.empty-cart p {
  color: #bfbfbf;
  font-size: 18px;
}

.cart-content {
  display: grid;
  grid-template-columns: 1fr 350px;
  gap: 40px;
}

.cart-items {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.cart-item {
  display: grid;
  grid-template-columns: 80px 1fr 120px 120px 40px;
  gap: 16px;
  align-items: center;
  background: #151519;
  border: 1px solid rgba(215, 181, 109, 0.15);
  border-radius: 12px;
  padding: 16px;
}

.item-image {
  width: 80px;
  height: 80px;
  object-fit: cover;
  border-radius: 8px;
}

.item-info h4 {
  margin: 0 0 8px;
  font-size: 16px;
}

.item-info p {
  margin: 0;
  color: #bfbfbf;
  font-size: 13px;
}

.item-controls {
  display: flex;
  align-items: center;
  gap: 8px;
}

.item-controls button {
  width: 28px;
  height: 28px;
  background: rgba(215, 181, 109, 0.2);
  border: 1px solid rgba(215, 181, 109, 0.3);
  color: #d7b56d;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 700;
  transition: 0.3s;
}

.item-controls button:hover {
  background: rgba(215, 181, 109, 0.4);
}

.item-controls input {
  width: 45px;
  text-align: center;
  background: #0f0f12;
  border: 1px solid rgba(215, 181, 109, 0.3);
  color: white;
  border-radius: 6px;
  padding: 4px;
}

.item-total {
  text-align: right;
  font-weight: 700;
  color: #d7b56d;
}

.remove-btn {
  background: none;
  border: none;
  color: #ff6b6b;
  cursor: pointer;
  font-size: 20px;
  transition: 0.3s;
}

.remove-btn:hover {
  transform: scale(1.2);
}

.cart-summary {
  background: #151519;
  border: 1px solid rgba(215, 181, 109, 0.15);
  border-radius: 12px;
  padding: 24px;
  height: fit-content;
  position: sticky;
  top: 100px;
}

.cart-summary h3 {
  margin: 0 0 20px;
  font-size: 20px;
}

.summary-row {
  display: flex;
  justify-content: space-between;
  margin-bottom: 12px;
  color: #bfbfbf;
  font-size: 14px;
}

.summary-total {
  display: flex;
  justify-content: space-between;
  padding-top: 12px;
  border-top: 1px solid rgba(215, 181, 109, 0.2);
  margin-bottom: 20px;
  font-weight: 700;
  color: #d7b56d;
}

.order-btn {
  width: 100%;
  padding: 12px;
  background: #d7b56d;
  color: black;
  border: none;
  border-radius: 8px;
  font-weight: 700;
  cursor: pointer;
  transition: 0.3s;
}

.order-btn:hover {
  background: #e5c578;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal {
  background: #151519;
  border: 1px solid rgba(215, 181, 109, 0.3);
  border-radius: 16px;
  padding: 32px;
  width: 90%;
  max-width: 500px;
  position: relative;
}

.close-btn {
  position: absolute;
  top: 12px;
  right: 12px;
  background: none;
  border: none;
  color: #ddd;
  font-size: 24px;
  cursor: pointer;
}

.modal h3 {
  margin: 0 0 24px;
  font-size: 24px;
}

.user-info {
  background: rgba(215, 181, 109, 0.1);
  border: 1px solid rgba(215, 181, 109, 0.2);
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 24px;
  font-size: 14px;
}

.user-info p {
  margin: 0 0 8px;
}

.modal form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.modal label {
  font-size: 14px;
  color: #bfbfbf;
  font-weight: 600;
}

.modal input {
  padding: 12px;
  border: 1px solid rgba(215, 181, 109, 0.3);
  border-radius: 8px;
  background: #0f0f12;
  color: white;
  font-size: 14px;
}

.modal input:focus {
  outline: none;
  border-color: #d7b56d;
}

.order-total {
  display: flex;
  justify-content: space-between;
  padding: 16px;
  background: rgba(215, 181, 109, 0.1);
  border-radius: 8px;
  font-weight: 700;
  color: #d7b56d;
}

.submit-btn {
  padding: 12px;
  background: #d7b56d;
  color: black;
  border: none;
  border-radius: 8px;
  font-weight: 700;
  cursor: pointer;
  transition: 0.3s;
  margin-top: 12px;
}

.submit-btn:hover {
  background: #e5c578;
}

@media (max-width: 900px) {
  .cart-content {
    grid-template-columns: 1fr;
  }

  .cart-item {
    grid-template-columns: 60px 1fr;
    gap: 12px;
  }

  .item-image {
    width: 60px;
    height: 60px;
    grid-column: 1;
    grid-row: 1 / 3;
  }

  .item-info {
    grid-column: 2;
  }

  .item-controls,
  .item-total,
  .remove-btn {
    grid-column: 1 / -1;
    justify-self: start;
  }

  .cart-summary {
    position: static;
  }
}
</style>