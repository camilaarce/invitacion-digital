<template>
    <div class="container">
    <h1 class="text-center mb-10">Mis fotos</h1>
    <div class="image-container">
    <div
          v-for="(foto, index) in evento.fotos"
          class="container-img"
          :key="index"
        >
          <img
            :src="foto"
            :alt="foto"
            :style="{ '--i': index }"
            class="animate"
          />
        </div>
        </div>
    </div>
</template>

<script setup>
import evento from "@/mocks/eventos.json";
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Lobster&display=swap');
.container {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 10%;
    background-color: rgb(226, 197, 160);
}
.image-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1%;
}

img {
  height: 30vh;
  aspect-ratio: 4/3;
  object-fit: cover;
}

h1 {
    font-family: 'Lobster', sans-serif;
    color: #496074;
    font-size: 60pt;
}

@media only screen and (max-width: 1000px) {
  .image-container {
    grid-template-columns: repeat(2, 1fr);
  }

  img {
  width: 45vw;
  height: auto;
}
}
</style>