<script setup>
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import WatchCatalog from './components/WatchCatalog.vue'
import About from './components/About.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="page">
    <Header />
    <Hero />
    <WatchCatalog />
    <About />
    <Footer />
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
</style>