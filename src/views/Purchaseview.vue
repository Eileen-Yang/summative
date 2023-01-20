<script setup>
import { ref } from 'vue';
import { useRouter } from "vue-router";
import { useStore } from '../store/index.js';
import SiteModal from '../components/SiteModal.vue';

const router = useRouter();
const showModal = ref(false);
const selectedId = ref(0);
const store = useStore();
const genre = ref()

const openModal = (id) => {
  showModal.value = true;
  selectedId.value = id;
};
const closeModal = () => {
  showModal.value = false;
};

const getGenres = async () => {
  await store.getMovies(genre.value);
}
</script>

<template>
  <div class="header-container">
    <h1>TRENDING MOVIES</h1>
    <RouterLink to="/cart" custom v-slot="{ navigate }">
      <button @click="navigate" role="link" class="cart"><i class="fa fa-shopping-cart"></i></button>
    </RouterLink>
  </div>
  <label>Search by Genre:</label>
  <select v-model="genre" @change="getGenres()" class="select-box">
    <option value="28">Action</option>
    <option value="12">Adventure</option>
    <option value="80">Crime</option>
    <option value="9648">Mystery</option>
    <option value="878">Science Fiction</option>
  </select>
  <div class="purchase-container">
    <img v-for="movie in store.movies" :id="movie.id" @click="openModal(movie.id)" class="poster"
      :src="`https://image.tmdb.org/t/p/w500${movie.poster}`" />
  </div>
  <SiteModal v-if="showModal" @toggleModal="closeModal()" :id="selectedId" />
</template>

<style scoped>
* {
  margin: 0px;
  padding: 1%;
}

.header-container {
  display: flex;
  justify-content: space-between;
  margin-top: 0.5%;
  margin-left: 0.05%;
}

h1 {
  font-size: 300%;
}

button {
  background-color: #c5c6c7;
  color: white;
  border-radius: 12px;
  font-size: 250%;
  cursor: pointer;
  width: fit-content;
  align-self: left;
  padding-right: 1.5%;
}

i {
  background-color: #c5c6c7;
  color: white;
}

label {
  font-size: 150%;
  margin-left: 1.5%;
}

select {
  width: 25%
}

option {
  font-size: 150%;
  padding: 0%;
}

.poster {
  width: 24%;
  aspect-ratio: 2/3;
  padding: 0.5%;
}

img:hover {
  cursor: pointer;
}
</style>