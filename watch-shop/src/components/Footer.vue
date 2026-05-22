<template>
  <footer class="footer">
    <div class="footer-content">
      <div class="footer-section">
        <h4>LUX WATCH</h4>
        <p>Премиум часы от ведущих мировых производителей</p>
      </div>

      <div class="footer-section">
        <h4>Навигация</h4>
        <button @click="$emit('navigate', 'home')" class="footer-link">Главная</button>
        <button @click="$emit('navigate', 'catalog')" class="footer-link">Каталог</button>
        <button @click="$emit('navigate', 'about')" class="footer-link">О компании</button>
        <button @click="$emit('navigate', 'contact')" class="footer-link">Контакты</button>
      </div>

      <div class="footer-section">
        <h4>Информация</h4>
        <a href="#" class="footer-link">Доставка и оплата</a>
        <a href="#" class="footer-link">Гарантия и возврат</a>
        <a href="#" class="footer-link">Политика конфиденциальности</a>
        <a href="#" class="footer-link">Условия использования</a>
      </div>

      <div class="footer-section">
        <h4>Контакты</h4>
        <p>
          +7 (495) 123-45-67<br>
          info@luxwatch.ru<br>
          г. Москва, ул. Арбат, 10
        </p>
      </div>
    </div>

    <div class="footer-bottom">
      <p>&copy; 2026 LUX WATCH. Все права защищены.</p>
      <div class="social">
        <a href="#">Вконтакте</a>
        <a href="#">Instagram</a>
        <a href="#">Telegram</a>
      </div>
    </div>
  </footer>
</template>

<script setup>
defineEmits(['navigate'])
</script>

<style scoped>
.footer {
  background: rgba(10, 10, 12, 0.95);
  border-top: 1px solid rgba(215, 181, 109, 0.2);
  color: white;
  padding: 40px 20px 20px;
  margin-top: 60px;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 32px;
}

.footer-section h4 {
  margin: 0 0 16px;
  font-size: 16px;
  color: #d7b56d;
}

.footer-section p {
  margin: 0;
  color: #bfbfbf;
  font-size: 14px;
  line-height: 1.6;
}

.footer-link {
  display: block;
  background: none;
  border: none;
  color: #bfbfbf;
  cursor: pointer;
  font-size: 14px;
  padding: 4px 0;
  transition: 0.3s;
  text-align: left;
  text-decoration: none;
}

.footer-link:hover {
  color: #d7b56d;
}

.footer-bottom {
  max-width: 1200px;
  margin: 0 auto;
  padding-top: 20px;
  border-top: 1px solid rgba(215, 181, 109, 0.1);
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 13px;
}

.footer-bottom p {
  margin: 0;
  color: #888;
}

.social {
  display: flex;
  gap: 20px;
}

.social a {
  color: #bfbfbf;
  text-decoration: none;
  transition: 0.3s;
}

.social a:hover {
  color: #d7b56d;
}

@media (max-width: 900px) {
  .footer-content {
    grid-template-columns: repeat(2, 1fr);
    gap: 24px;
  }

  .footer-bottom {
    flex-direction: column;
    gap: 16px;
    text-align: center;
  }

  .social {
    justify-content: center;
  }
}

@media (max-width: 600px) {
  .footer-content {
    grid-template-columns: 1fr;
  }
}
</style>