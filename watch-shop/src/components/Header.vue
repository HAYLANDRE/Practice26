<template>
  <header class="header">
    <div class="logo">LUX WATCH</div>

    <nav class="menu">
      <a href="#catalog">Каталог</a>
      <a href="#about">О бренде</a>
      <a href="#contacts">Контакты</a>
    </nav>
  </header>
</template>

<style scoped>
.header {
  height: 78px;
  padding: 0 60px;
  display: flex;
  align-items: center;
  justify-content: space-between;

  background: rgba(10, 10, 12, 0.9);
  border-bottom: 1px solid rgba(255,255,255,0.08);

  position: sticky;
  top: 0;
  z-index: 100;
}

.logo {
  font-size: 24px;
  font-weight: 900;
  letter-spacing: 2px;
  color: #d7b56d;
}

.menu {
  display: flex;
  gap: 26px;
}

.menu a {
  color: #ddd;
  text-decoration: none;
  font-weight: 700;
}

.menu a:hover {
  color: #d7b56d;
}
</style>