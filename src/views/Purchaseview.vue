<script setup>
import { ref } from 'vue';
import { useRouter } from "vue-router";
import { useStore } from '../store/index.js'
import SiteModal from '../components/SiteModal.vue';
import SiteFooter from '../components/SiteFooter.vue'

const router = useRouter();
const showModal = ref(false);
const selectedId = ref(0);
const store = useStore();
const genre = ref(12)

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
  <RouterLink to="/cart" custom v-slot="{ navigate }">
    <button @click="navigate" role="link" class="cart">CART</button>
  </RouterLink>
  <h1>TRENDING MOVIES</h1>
  <select v-model="genre" @change="getGenres()">
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
  <Suspense>
    <SiteFooter />
  </Suspense>
</template>

<style scoped>
h1 {
  padding-left: 1.5%;
  padding-right: 64%;
  font-size: 300%;
}

.poster {
  width: 24%;
  aspect-ratio: 2/3;
  padding: 0.5%;
}

img:hover {
  cursor: pointer;
}

button {
  font-size: 200%;
  background-color: #c5c6c7;
  color: white;
  border-radius: 12px;
  margin-top: 1%;
  cursor: pointer;
}

.SiteFooter {
  font-size: 100%;
}
</style>