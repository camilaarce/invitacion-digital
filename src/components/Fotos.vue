<template>
  <div class="container contenedor-fotos">
    <div class="imagen"></div>
    <Transition name="slide" mode="out-in">
      <h1 v-if="transitionImage" class="text-center mb-10">Mis fotos</h1>
    </Transition>
    <div class="image-container">
      <div
        v-for="(foto, index) in evento.fotos"
        class="container-img"
        :key="index"
      >
        <Transition name="slide" mode="out-in">
          <img
            v-if="transitionImage"
            :src="foto"
            :alt="foto"
            :style="{ '--i': index }"
            loading="lazy"
          />
        </Transition>
      </div>
    </div>
  </div>
</template>

<script setup>
import evento from "@/mocks/eventos.json";
import { onMounted } from "vue";
import { ref } from "vue";

const transitionImage = ref(false);
const observer = ref(null);
onMounted(() => {
  setInterval(() => {
    const options = {
      root: null,
      rootMargin: "0px",
      threshold: 0.5,
    };
    const handleIntersection = (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          transitionImage.value = true;
          observer.value.disconnect();
        } else {
          transitionImage.value = false;
        }
      });
    };
    observer.value = new IntersectionObserver(handleIntersection, options);
    observer.value.observe(document.querySelector(".imagen"));
  }, 1000);
});
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Lobster&display=swap");

.container {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: #e2c5a0;
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
  transition: all 1s ease;
}

img:hover {
  height: 40vh;
  transition: all 1s ease;
}

h1 {
  font-family: "Lobster", sans-serif;
  color: #496074;
  font-size: 60pt;
}

.slide-enter-active,
.slide-leave-active {
  transition: all 1s ease;
  transition-delay: calc(0.2s * var(--i));
}

.slide-enter-from,
.slide-leave-to {
  opacity: 0;
  filter: blur(10px);
  transform: translateX(100px);
}

@media only screen and (max-width: 1100px) {
  .image-container {
    grid-template-columns: repeat(2, 1fr);
  }

  img {
    width: 45vw;
    height: auto;
  }
}
</style>