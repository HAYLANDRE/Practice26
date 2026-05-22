<script setup>
import { ref, computed } from 'vue'
import Header from './components/Header.vue'
import Home from './components/Home.vue'
import Catalog from './components/Catalog.vue'
import About from './components/About.vue'
import Contact from './components/Contact.vue'
import Cart from './components/Cart.vue'
import Footer from './components/Footer.vue'

const currentPage = ref('home')
const cart = ref([])
const user = ref(null)
const showRegisterModal = ref(false)
const formData = ref({ name: '', email: '', phone: '' })
const errors = ref({ name: '', email: '', phone: '' })

const cartCount = computed(() => cart.value.length)

const validateForm = () => {
  errors.value = { name: '', email: '', phone: '' }

  const name = formData.value.name.trim()
  const email = formData.value.email.trim()
  const phone = formData.value.phone.trim()

  if (!name) {
    errors.value.name = 'Имя обязательно'
  } else if (name.length < 2) {
    errors.value.name = 'Имя должно быть минимум 2 символа'
  } else if (name.length > 50) {
    errors.value.name = 'Имя не должно быть больше 50 символов'
  }

  if (!email) {
    errors.value.email = 'Email обязателен'
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) {
    errors.value.email = 'Некорректный email адрес'
  }

  if (!phone) {
    errors.value.phone = 'Телефон обязателен'
  } else if (!/^\d{10,}$/.test(phone.replace(/\D/g, ''))) {
    errors.value.phone = 'Телефон должен содержать минимум 10 цифр'
  }

  return !errors.value.name && !errors.value.email && !errors.value.phone
}

const addToCart = (product) => {
  const existing = cart.value.find(item => item.id === product.id)
  if (existing) {
    existing.quantity++
  } else {
    cart.value.push({ ...product, quantity: 1 })
  }
}

const removeFromCart = (productId) => {
  cart.value = cart.value.filter(item => item.id !== productId)
}

const updateQuantity = (productId, quantity) => {
  const item = cart.value.find(item => item.id === productId)
  if (item) {
    item.quantity = Math.max(1, quantity)
  }
}

const registerUser = (userData) => {
  user.value = userData
  showRegisterModal.value = false
}

const handleRegister = () => {
  if (!validateForm()) {
    return
  }

  registerUser({
    name: formData.value.name.trim(),
    email: formData.value.email.trim(),
    phone: formData.value.phone.trim(),
    registeredAt: new Date().toLocaleDateString('ru-RU')
  })
  formData.value = { name: '', email: '', phone: '' }
  errors.value = { name: '', email: '', phone: '' }
}

const logout = () => {
  user.value = null
  cart.value = []
}

const navigateTo = (page) => {
  currentPage.value = page
}
</script>

<template>
  <div class="app">
    <Header
      :current-page="currentPage"
      :cart-count="cartCount"
      :user="user"
      @navigate="navigateTo"
      @show-register="showRegisterModal = true"
      @logout="logout"
    />

    <main class="main-content">
      <Home v-if="currentPage === 'home'" @navigate="navigateTo" />
      <Catalog
        v-if="currentPage === 'catalog'"
        @add-to-cart="addToCart"
      />
      <About v-if="currentPage === 'about'" />
      <Contact v-if="currentPage === 'contact'" />
      <Cart
        v-if="currentPage === 'cart'"
        :cart="cart"
        :user="user"
        @remove="removeFromCart"
        @update-quantity="updateQuantity"
        @show-register="showRegisterModal = true"
      />
    </main>

    <Footer @navigate="navigateTo" />

    <!-- Register Modal -->
    <div v-if="showRegisterModal" class="modal-overlay" @click="showRegisterModal = false">
      <div class="modal" @click.stop>
        <button class="close-btn" @click="showRegisterModal = false">✕</button>
        <h2>Регистрация</h2>
        <form @submit.prevent="handleRegister">
          <div class="form-group">
            <label>Ваше имя</label>
            <input
              v-model="formData.name"
              type="text"
              placeholder="Введите имя (минимум 2 символа)"
              @blur="validateForm"
            >
            <span v-if="errors.name" class="error-text">{{ errors.name }}</span>
          </div>

          <div class="form-group">
            <label>Email</label>
            <input
              v-model="formData.email"
              type="email"
              placeholder="Введите корректный email"
              @blur="validateForm"
            >
            <span v-if="errors.email" class="error-text">{{ errors.email }}</span>
          </div>

          <div class="form-group">
            <label>Телефон</label>
            <input
              v-model="formData.phone"
              type="tel"
              placeholder="Введите номер телефона (10+ цифр)"
              @blur="validateForm"
            >
            <span v-if="errors.phone" class="error-text">{{ errors.phone }}</span>
          </div>

          <button type="submit" class="submit-btn">Зарегистрироваться</button>
        </form>
      </div>
    </div>
  </div>
</template>

<style>
body {
  margin: 0;
  background:
    radial-gradient(circle at top left, rgba(190, 145, 60, 0.18), transparent 35%),
    #0b0b0d;
  font-family: Arial, sans-serif;
}

.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background: linear-gradient(135deg, #0f0f12 0%, #1a1a1f 100%);
}

.main-content {
  flex: 1;
  max-width: 1200px;
  width: 100%;
  margin: 0 auto;
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
  max-width: 450px;
  color: white;
  position: relative;
  max-height: 90vh;
  overflow-y: auto;
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
  transition: 0.3s;
}

.close-btn:hover {
  color: #d7b56d;
}

.modal h2 {
  margin: 0 0 24px;
  text-align: center;
  font-size: 28px;
}

.modal form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form-group label {
  font-size: 14px;
  color: #d7b56d;
  font-weight: 600;
}

.modal input {
  padding: 12px;
  border: 1px solid rgba(215, 181, 109, 0.3);
  border-radius: 8px;
  background: #0f0f12;
  color: white;
  font-size: 14px;
  transition: 0.3s;
}

.modal input::placeholder {
  color: #666;
}

.modal input:focus {
  outline: none;
  border-color: #d7b56d;
  box-shadow: 0 0 0 2px rgba(215, 181, 109, 0.1);
}

.error-text {
  font-size: 12px;
  color: #ff6b6b;
  font-weight: 600;
  margin-top: -2px;
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
  margin-top: 8px;
  font-size: 15px;
}

.submit-btn:hover {
  background: #e5c578;
  transform: translateY(-2px);
}

.submit-btn:active {
  transform: translateY(0);
}
</style>