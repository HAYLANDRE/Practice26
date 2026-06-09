<template>
  <header class="header">
    <div class="logo" @click="$emit('navigate', 'home')">LUX WATCH</div>

    <nav class="menu">
      <button
        @click="$emit('navigate', 'home')"
        :class="{ active: currentPage === 'home' }"
        class="nav-btn"
      >
        Главная
      </button>
      <button
        @click="$emit('navigate', 'catalog')"
        :class="{ active: currentPage === 'catalog' }"
        class="nav-btn"
      >
        Каталог
      </button>
      <button
        @click="$emit('navigate', 'about')"
        :class="{ active: currentPage === 'about' }"
        class="nav-btn"
      >
        О компании
      </button>
      <button
        @click="$emit('navigate', 'contact')"
        :class="{ active: currentPage === 'contact' }"
        class="nav-btn"
      >
        Обратная связь
      </button>
    </nav>

    <div class="right-section">
      <div class="cart-icon" @click="$emit('navigate', 'cart')">
        🛒
        <span v-if="cartCount > 0" class="cart-badge">{{ cartCount }}</span>
      </div>

     <div v-if="user" class="user-menu">
  <span class="user-name">{{ user.name }}</span>

  <button
    @click="$emit('navigate', 'profile')"
    class="profile-btn"
  >
    Личный кабинет
  </button>

  <button @click="$emit('logout')" class="logout-btn">
    Выход
  </button>
</div>
      <button v-else @click="$emit('show-register')" class="login-btn">
        Вход/Регистр.
      </button>
    </div>
  </header>
</template>

<script setup>
defineProps({
  currentPage: String,
  cartCount: Number,
  user: Object
})

defineEmits(['navigate', 'show-register', 'logout'])
</script>

<style scoped>
.profile-btn {
  background: none;
  border: 1px solid #d7b56d;
  color: #d7b56d;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 12px;
}

.profile-btn:hover {
  background: #d7b56d;
  color: black;
}
.header {
  height: 70px;
  padding: 0 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: rgba(10, 10, 12, 0.95);
  border-bottom: 1px solid rgba(215, 181, 109, 0.2);
  position: sticky;
  top: 0;
  z-index: 100;
}

.logo {
  font-size: 22px;
  font-weight: 900;
  letter-spacing: 2px;
  color: #d7b56d;
  cursor: pointer;
  transition: 0.3s;
}

.logo:hover {
  color: #e5c578;
}

.menu {
  display: flex;
  gap: 8px;
  flex: 1;
  justify-content: center;
}

.nav-btn {
  background: none;
  border: none;
  color: #ddd;
  font-weight: 600;
  padding: 8px 16px;
  cursor: pointer;
  border-radius: 6px;
  transition: 0.3s;
  font-size: 14px;
}

.nav-btn:hover {
  background: rgba(215, 181, 109, 0.1);
  color: #d7b56d;
}

.nav-btn.active {
  background: rgba(215, 181, 109, 0.2);
  color: #d7b56d;
}

.right-section {
  display: flex;
  align-items: center;
  gap: 16px;
}

.cart-icon {
  font-size: 24px;
  cursor: pointer;
  position: relative;
  transition: 0.3s;
}

.cart-icon:hover {
  transform: scale(1.1);
}

.cart-badge {
  position: absolute;
  top: -8px;
  right: -8px;
  background: #d7b56d;
  color: black;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  font-weight: 700;
}

.user-menu {
  display: flex;
  align-items: center;
  gap: 12px;
}

.user-name {
  color: #d7b56d;
  font-size: 14px;
  font-weight: 600;
}

.logout-btn {
  background: none;
  border: 1px solid #d7b56d;
  color: #d7b56d;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 12px;
  transition: 0.3s;
}

.logout-btn:hover {
  background: #d7b56d;
  color: black;
}

.login-btn {
  background: #d7b56d;
  color: black;
  border: none;
  padding: 8px 16px;
  border-radius: 6px;
  font-weight: 600;
  cursor: pointer;
  transition: 0.3s;
  font-size: 13px;
}

.login-btn:hover {
  background: #e5c578;
}

@media (max-width: 900px) {
  .header {
    padding: 0 20px;
    gap: 12px;
  }

  .menu {
    display: none;
  }

  .nav-btn {
    padding: 6px 10px;
    font-size: 12px;
  }
}
</style>