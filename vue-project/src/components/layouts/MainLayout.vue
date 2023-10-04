<template>
  <div>
    <Header />
    <Slider />
    <router-view></router-view>
    <Navbar />
    <Footer />
  </div>
</template>

<script setup>
import Header from "../layouts/Header.vue";
import Slider from "../layouts/Slider.vue";
import Navbar from "../layouts/Navbar.vue";
import Footer from "../layouts/Footer.vue";
</script>
