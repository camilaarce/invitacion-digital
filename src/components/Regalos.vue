<template>
  <div class="container">
    <div class="regalo"></div>
    <Transition name="zoom" mode="out-in">
      <h1 v-if="transitionRegalos">Regalos</h1>
    </Transition>
    <Transition name="fade" mode="out-in">
      <h3 v-if="transitionRegalos" class="text-center mb-5">
        ¿Te gustaría regalarme algo más, aparte de tu maravillosa presencia?
      </h3>
    </Transition>
    <v-dialog width="600">
      <template v-slot:activator="{ props }">
        <Transition name="slide" mode="out-in">
          <v-btn
            v-if="transitionRegalos"
            size="x-large"
            width="400"
            height="60"
            variant="flat"
            color="#003b6e"
            v-bind="props"
            append-icon="mdi-gift"
            >regalos</v-btn
          ></Transition
        >
      </template>
      <template v-slot:default="{ isActive }">
        <v-card style="padding: 5%">
          <v-card-text class="text-center">
            <v-icon
              icon="mdi-gift-outline"
              class="wobble-hor-bottom"
              size="100"
            ></v-icon>
            <h2>Lo más importante para mí es tu presencia</h2>
            <h2>pero si deseas hacerme un regalo aquí te dejo los datos</h2>
            <h2 class="mt-3">CBU: {{ evento.cbu }}</h2>
            <h2>Alias: {{ evento.alias }}</h2>
            <h2>{{ evento.titular }}</h2>
          </v-card-text>
          <v-card-actions class="justify-end">
            <v-btn variant="text" @click="isActive.value = false">cerrar</v-btn>
          </v-card-actions>
        </v-card>
      </template>
    </v-dialog>
  </div>
</template>

<script setup>
import evento from "@/mocks/eventos.json";

import { ref, onMounted } from "vue";

const transitionRegalos = ref(false);

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
          transitionRegalos.value = true;
          observer.value.disconnect();
        } else {
          transitionRegalos.value = false;
        }
      });
    };

    observer.value = new IntersectionObserver(handleIntersection, options);

    observer.value.observe(document.querySelector(".regalo"));
  }, 1000);
});
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Lobster&display=swap");

.container {
  height: 60vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: beige;
}

h1 {
  font-family: "Lobster", sans-serif;
  font-size: 90pt;
  color: rgb(51, 94, 94);
}

h3 {
  color: rgb(126, 50, 0);
  font-size: 30pt;
}

.wobble-hor-bottom {
  animation: wobble-hor-bottom 2s infinite both;
}

@keyframes wobble-hor-bottom {
  0%,
  100% {
    transform: translateX(0%);
    transform-origin: 50% 50%;
  }
  15% {
    transform: translateX(-30px) rotate(-6deg);
  }
  30% {
    transform: translateX(15px) rotate(6deg);
  }
  45% {
    transform: translateX(-15px) rotate(-3.6deg);
  }
  60% {
    transform: translateX(9px) rotate(2.4deg);
  }
  75% {
    transform: translateX(-6px) rotate(-1.2deg);
  }
}

.zoom-enter-active,
.zoom-leave-active {
  transition: all 1s ease;
}

.zoom-enter-from,
.zoom-leave-to {
  opacity: 0;
  filter: blur(10px);
  transform: scale(0);
}

.fade-enter-active,
.fade-leave-active {
  transition: all 1s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  filter: blur(10px);
  transform: translateX(-100px);
}

.slide-enter-active,
.slide-leave-active {
  transition: all 1s ease;
}

.slide-enter-from,
.slide-leave-to {
  opacity: 0;
  filter: blur(10px);
  transform: translateY(-100%);
}
</style>