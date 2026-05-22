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

const cartCount = computed(() => cart.value.length)

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
  registerUser({
    name: formData.value.name,
    email: formData.value.email,
    phone: formData.value.phone,
    registeredAt: new Date().toLocaleDateString('ru-RU')
  })
  formData.value = { name: '', email: '', phone: '' }
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
          <input v-model="formData.name" type="text" placeholder="Ваше имя" required>
          <input v-model="formData.email" type="email" placeholder="Email" required>
          <input v-model="formData.phone" type="tel" placeholder="Телефон" required>
          <button type="submit">Зарегистрироваться</button>
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
  max-width: 400px;
  color: white;
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

.modal input {
  padding: 12px;
  border: 1px solid rgba(215, 181, 109, 0.3);
  border-radius: 8px;
  background: #0f0f12;
  color: white;
  font-size: 14px;
}

.modal input::placeholder {
  color: #888;
}

.modal input:focus {
  outline: none;
  border-color: #d7b56d;
}

.modal button[type="submit"] {
  padding: 12px;
  background: #d7b56d;
  color: black;
  border: none;
  border-radius: 8px;
  font-weight: 700;
  cursor: pointer;
  transition: 0.3s;
}

.modal button[type="submit"]:hover {
  background: #e5c578;
}
</style>