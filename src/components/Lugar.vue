<template>
  <div class="container contenedor-lugar">
    <Transition name="zoom" mode="out-in">
      <h1 v-if="transitionLugar" class="mb-5 text-center">¿Dónde y cuándo?</h1>
    </Transition>
    <Transition name="fade" mode="out-in">
      <div v-if="transitionLugar">
        <h3 class="text-center">{{ evento.address }}</h3>
        <h3 class="mb-5 text-center">{{ evento.horario }}</h3>
      </div>
    </Transition>
    <Transition name="slide" mode="out-in">
      <v-btn
        v-if="transitionLugar"
        size="x-large"
        width="400"
        height="60"
        variant="flat"
        color="#003b6e"
        append-icon="mdi-send"
        ><a
          href="https://www.google.com/maps/place/Plaza+Libertad+Santiago+del+Estero/@-27.7938176,-64.2547712,14z/data=!4m6!3m5!1s0x943b52116541bda1:0x63357d1eff4af526!8m2!3d-27.7875278!4d-64.2595019!16s%2Fg%2F1tkkvzln?entry=ttu"
          target="_blank"
          >Ver en maps</a
        ></v-btn
      >
    </Transition>
    <div class="lugar"></div>
  </div>
</template>

<script setup>
import evento from "@/mocks/eventos.json";
import { ref, onMounted } from "vue";

const transitionLugar = ref(false);

onMounted(() => {
  setInterval(() => {
    const contenedor = document.querySelector(".contenedor-lugar");

    const rect = contenedor.getBoundingClientRect();

    if (
      rect.top >= 0 &&
      rect.left >= 0 &&
      rect.bottom <=
        (window.innerHeight || document.documentElement.clientHeight) &&
      rect.right <= (window.innerWidth || document.documentElement.clientWidth)
    ) {
      transitionLugar.value = true;
    } else {
      transitionLugar.value = false;
    }
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
  background-color: rgb(173, 233, 233);
}

h1 {
  font-family: "Lobster", sans-serif;
  color: #96794f;
  font-size: 60pt;
}

h3 {
  font-size: 25pt;
  color: rgb(97, 97, 97);
}

a {
  text-decoration: none;
  color: #ffffff;
}

.zoom-enter-active,
.zoom-leave-active {
  transition: all 1s ease;
}

.zoom-enter-from,
.zoom-leave-to {
  opacity: 0;
  filter: blur(10px);
  transform: scale(1.5);
}

.fade-enter-active,
.fade-leave-active {
  transition: all 1s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  filter: blur(10px);
  transform: translateX(100px);
}

.slide-enter-active,
.slide-leave-active {
  transition: all 1s ease;
}

.slide-enter-from,
.slide-leave-to {
  opacity: 0;
  filter: blur(10px);
  transform: translateY(100%);
}
</style>