<script setup>
import axios from "axios";
import { useStore } from '../store/index.js'

const props = defineProps(["id"]);
const emits = defineEmits(["toggleModal"]);
const store = useStore();

let data = (await axios.get(`https://api.themoviedb.org/3/movie/${props.id}`, {
  params: {
    api_key: '289d7511f89338dfaa9d5bc06621094c',
    append_to_response: "videos",
  }
})).data;
console.log(data);

function Opentab() {
  window.open(url);
}

</script>

<template>
  <Teleport to="body">
    <div class="modal-outer-container" @click.self="emits('toggleModal')">
      <div class="modal-inner-container">
        <button class="close-button" @click="emits('toggleModal')">X</button>
        <img :src="`https://image.tmdb.org/t/p/w500/${data.poster_path}`" />
        <div class="movie-information">
          <h2>{{ data.title }}</h2>
          <h3>Release Date: {{ data.release_date }}</h3>
          <h3>Overview: {{ data.overview }}</h3>
          <h4 @click="Opentab"><a :href="`https://www.youtube.com/watch?v=${data.videos.results[0].key}`" target="_blank">Movie Trailer</a></h4>
          <button
          @click="
            store.addToCart(props.id, {
              id: data.id,
              poster: data.poster_path,
              title: data.title,
              date: data.release_date,
              tagline: data.tagline,
              overview: data.overview,
            })
          "
        >
          Purchase
        </button>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
* {
  background-color: #1F2123;
  margin-top: 0%;
}

.modal-outer-container {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background: #00000099;
  z-index: 3;
}

.modal-outer-container .modal-inner-container {
  color: white;
  width: clamp(280px, 100%, 800px);
  height: 400px;
  position: relative;
  display: flex;
}

.modal-outer-container .modal-inner-container .close-button {
  position: absolute;
  right: 0px;
  padding: 1rem;
  border: none;
  background: #1F2123;
  font-weight: bold;
  font-size: 1.25rem;
  color: white;
}

h2 {
  font-size: 200%;
}

h3 {
  color: white;
}

img {
  aspect-ratio: 2/3;
  padding: 2%;
}

.movie-information {
  padding-top: 2%;
  padding-right: 2%;
  display: flex;
  flex-direction: column;
  width: 60%;
}

button {
  font-size: 200%;
  background-color: #c5c6c7;
  color: white;
  border-radius: 12px;
  margin-top: 1%;
  cursor: pointer;
}
</style>
