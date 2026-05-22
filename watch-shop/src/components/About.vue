<template>
  <section id="about" class="about">
    <h2>О коллекции</h2>

    <p>
      LUX WATCH — это каталог часов в премиальном стиле. Здесь представлены
      модели для делового образа, повседневного использования и особых случаев.
    </p>

    <div class="features">
      <div>
        <h3>Качество</h3>
        <p>Надёжные материалы и точные механизмы.</p>
      </div>

      <div>
        <h3>Стиль</h3>
        <p>Современный дизайн и классические формы.</p>
      </div>

      <div>
        <h3>Выбор</h3>
        <p>Модели для разных задач и образов.</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  max-width: 1100px;
  margin: 0 auto 80px;
  padding: 40px;
  border-radius: 24px;
  background: rgba(255, 255, 255, 0.06);
  color: white;
}

.about h2 {
  font-size: 38px;
  margin: 0 0 18px;
}

.about p {
  color: #cfcfcf;
  font-size: 18px;
  line-height: 1.7;
}

.features {
  margin-top: 30px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;
}

.features div {
  padding: 22px;
  border-radius: 18px;
  background: #151519;
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.features h3 {
  color: #d7b56d;
  margin-top: 0;
}

@media (max-width: 900px) {
  .features {
    grid-template-columns: 1fr;
  }
}
</style>