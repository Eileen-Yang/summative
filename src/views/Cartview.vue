<script setup>
import { useStore } from "../store/index.js";
const store = useStore();
</script>

<template>
  <h1>CART</h1>
  <div v-for="movie in Array.from(store.cart.values())" class="cart-container">
    <img :src="`https://image.tmdb.org/t/p/w500${movie.poster}`" />
    <div class="movie-info">
      <h2>{{ movie.title }}</h2>
      <h3>{{ movie.date }}</h3>
      <h4>"{{ movie.tagline }}"</h4>
      <button @click="store.removeFromCart(movie.id)">Remove</button>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0px;
  padding: 1%;
}

h1 {
  font-size: 300%;
  margin-top: 1.5%;
  margin-left: 0.75%;
}

.cart-container {
  display: flex;
}

img {
  aspect-ratio: 2 / 3;
  width: 15%;
}

.movie-info {
  display: flex;
  flex-direction: column;
  padding-top: 2%;
  padding-right: 2%;
  font-size: 150%;
  width: 80%;
}

button {
  background-color: #c5c6c7;
  color: white;
  border-radius: 12px;
  font-size: 150%;
  cursor: pointer;
  width: fit-content;
  align-self: left;
  margin-top: 2%;
}
</style>