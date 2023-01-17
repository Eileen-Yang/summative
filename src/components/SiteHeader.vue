<script setup>
</script>

<template>
  <div class="header-container">
    <h1>XYZ MOVIES</h1>
    <RouterLink to="/login" custom v-slot="{ navigate }">
      <button @click="navigate" role="link">LOGIN</button>
    </RouterLink>
  </div>
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
  font-size: 150%;
}
</style>