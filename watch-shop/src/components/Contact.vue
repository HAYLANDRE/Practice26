<script setup>
import { ref } from 'vue'

const form = ref({
  name: '',
  email: '',
  message: ''
})

const submitted = ref(false)

const handleSubmit = () => {
  submitted.value = true
  form.value = { name: '', email: '', message: '' }
  setTimeout(() => {
    submitted.value = false
  }, 3000)
}
</script>

<template>
  <section class="contact">
    <h2>Обратная связь</h2>

    <div class="contact-content">
      <div class="contact-info">
        <div class="info-item">
          <h3>📍 Адрес</h3>
          <p>г. Москва, ул. Арбат, дом 10<br>Офис 305</p>
        </div>

        <div class="info-item">
          <h3>📞 Телефон</h3>
          <p>+7 (495) 123-45-67<br>Пн-Пт: 10:00 - 18:00</p>
        </div>

        <div class="info-item">
          <h3>📧 Email</h3>
          <p>info@luxwatch.ru<br>support@luxwatch.ru</p>
        </div>

        <div class="info-item">
          <h3>🕐 Часы работы</h3>
          <p>Пн-Сб: 10:00 - 20:00<br>Вс: 11:00 - 19:00</p>
        </div>
      </div>

      <form @submit.prevent="handleSubmit" class="contact-form">
        <h3>Отправить сообщение</h3>

        <div v-if="submitted" class="success-message">
          ✓ Спасибо! Ваше сообщение отправлено. Мы свяжемся с вами в течение 24 часов.
        </div>

        <input
          v-model="form.name"
          type="text"
          placeholder="Ваше имя"
          required
        >

        <input
          v-model="form.email"
          type="email"
          placeholder="Email"
          required
        >

        <textarea
          v-model="form.message"
          placeholder="Ваше сообщение"
          rows="6"
          required
        ></textarea>

        <button type="submit">Отправить</button>
      </form>
    </div>
  </section>
</template>

<style scoped>
.contact {
  padding: 60px 20px;
  color: white;
}

.contact h2 {
  margin: 0 0 40px;
  font-size: 38px;
  text-align: center;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  max-width: 1000px;
  margin: 0 auto;
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.info-item {
  background: rgba(215, 181, 109, 0.08);
  border: 1px solid rgba(215, 181, 109, 0.15);
  border-radius: 12px;
  padding: 24px;
}

.info-item h3 {
  margin: 0 0 12px;
  font-size: 18px;
}

.info-item p {
  margin: 0;
  color: #bfbfbf;
  line-height: 1.8;
}

.contact-form {
  background: rgba(215, 181, 109, 0.08);
  border: 1px solid rgba(215, 181, 109, 0.15);
  border-radius: 12px;
  padding: 28px;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.contact-form h3 {
  margin: 0 0 16px;
  font-size: 22px;
}

.success-message {
  padding: 16px;
  background: rgba(76, 175, 80, 0.2);
  border: 1px solid rgba(76, 175, 80, 0.5);
  border-radius: 8px;
  color: #80e080;
  font-size: 14px;
  text-align: center;
}

.contact-form input,
.contact-form textarea {
  background: #0f0f12;
  border: 1px solid rgba(215, 181, 109, 0.3);
  border-radius: 8px;
  padding: 12px;
  color: white;
  font-family: inherit;
  font-size: 14px;
}

.contact-form input::placeholder,
.contact-form textarea::placeholder {
  color: #666;
}

.contact-form input:focus,
.contact-form textarea:focus {
  outline: none;
  border-color: #d7b56d;
}

.contact-form button {
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

.contact-form button:hover {
  background: #e5c578;
}

@media (max-width: 900px) {
  .contact-content {
    grid-template-columns: 1fr;
  }

  .contact h2 {
    font-size: 28px;
  }
}
</style>