<template>
  <div class="container">
    <div class="name"></div>
    <Transition name="fade" mode="out-in">
      <h1 v-if="transitionName">{{ evento.name }}</h1>
    </Transition>
    <Transition name="slide" mode="out-in">
      <h2 v-if="transitionName">
        <v-row>
          <v-col cols="3">
            <p class="text-center">{{ tiempoRestante.dias }}</p>
            <p class="text-center">
              {{ tiempoRestante.dias == 1 ? "dia" : "dias" }}
            </p>
          </v-col>
          <v-col cols="3">
            <p class="text-center">{{ tiempoRestante.horas }}</p>
            <p class="text-center">hs</p>
          </v-col>
          <v-col cols="3">
            <p class="text-center">{{ tiempoRestante.minutos }}</p>
            <p class="text-center">min</p>
          </v-col>
          <v-col cols="3">
            <p class="text-center">{{ tiempoRestante.segundos }}</p>
            <p class="text-center">seg</p>
          </v-col>
        </v-row>
      </h2>
    </Transition>
  </div>
</template>

<script setup>
import evento from "@/mocks/eventos.json";
import { ref, onMounted, onUnmounted } from "vue";

const transitionName = ref(false);
const tiempoRestante = ref({
  dias: "00",
  horas: "00",
  minutos: "00",
  segundos: "00",
});

const interval = ref(0);

const calcularTiempoRestante = () => {
  const fechaObjetivo = evento.date;
  const now = new Date();
  const target = new Date(fechaObjetivo.replace(" ", "T"));
  const diferencia = target - now;

  if (diferencia < 0) {
    tiempoRestante.value = {
      dias: "00",
      horas: "00",
      minutos: "00",
      segundos: "00",
    };
    clearInterval(interval.value);
    return;
  }

  tiempoRestante.value.dias = Math.floor(diferencia / (1000 * 60 * 60 * 24));
  tiempoRestante.value.horas = String(
    Math.floor((diferencia % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
  ).padStart(2, "0");
  tiempoRestante.value.minutos = String(
    Math.floor((diferencia % (1000 * 60 * 60)) / (1000 * 60))
  ).padStart(2, "0");
  tiempoRestante.value.segundos = String(
    Math.floor((diferencia % (1000 * 60)) / 1000)
  ).padStart(2, "0");
};

const observer = ref(null);

onMounted(() => {
  calcularTiempoRestante();
  interval.value = setInterval(calcularTiempoRestante, 1000);

  setInterval(() => {
    const options = {
      root: null,
      rootMargin: "0px",
      threshold: 0.5,
    };

    const handleIntersection = (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          transitionName.value = true;
          observer.value.disconnect();
        } else {
          transitionName.value = false;
        }
      });
    };

    observer.value = new IntersectionObserver(handleIntersection, options);

    observer.value.observe(document.querySelector(".name"));
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
  font-size: 100pt;
  color: rgb(51, 94, 94);
}

h2 {
  color: rgb(126, 50, 0);
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
  transform: translateX(100px);
}
</style>