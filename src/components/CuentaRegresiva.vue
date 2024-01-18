<template>
  <div class="image--container contenedor-nombre">
    <div class="kenburns-top"></div>
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
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: beige;
  overflow: hidden;
}

.image--container {
  position: relative;
  height: 100%;
  overflow: hidden;
}

.kenburns-top {
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background: url("https://i.ibb.co/ftvBfK4/foto6.jpg") center/cover no-repeat;
  animation: kenburns-top 5s ease-in-out infinite alternate-reverse both;
  filter: brightness(0.3);
}

@keyframes kenburns-top {
  0% {
    transform: scale(1) translateY(0);
    transform-origin: 50% 16%;
  }

  100% {
    transform: scale(1.25) translateY(-15px);
    transform-origin: top;
  }
}

h1 {
  font-family: "Lobster", sans-serif;
  font-size: 90pt;
  color: rgb(51, 94, 94);
  z-index: 10;
  text-shadow: 0 0 10px #ffffff82, 0 0 30px #ffffff82, 0 0 0px #ffffff82;
  padding: 2%;
}

h2 {
  color: rgb(169, 109, 68);
  z-index: 10;
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