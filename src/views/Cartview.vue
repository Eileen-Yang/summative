<script setup>
import { useStore } from "../store/index.js";
const store = useStore();
</script>

<template>
  <div v-for="movie in Array.from(store.cart.values())" class="cart-container">
    <img :src="`https://image.tmdb.org/t/p/w500${movie.poster}`" />
    <div class="info-container">
      <h1>{{ movie.title }}</h1>
      <h2>{{ movie.date }}</h2>
      <h3>"{{ movie.tagline }}"</h3>
      <button @click="store.removeFromCart(movie.id)">Remove</button>
    </div>
  </div>
</template>

<style scoped>
img {
  aspect-ratio: 2 / 3;
  width: 20%;
}

.cart-container {
  display: flex;
}

.info-container {
  display: flex;
  flex-direction: column;
  width: 50%;
}
</style>