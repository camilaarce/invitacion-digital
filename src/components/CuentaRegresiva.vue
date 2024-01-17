<template>
    <div class="container">
        <h1>{{ evento.name }}</h1>
      <h3>
        <v-row>
            <v-col cols="3">
                <p class="text-center">{{ tiempoRestante.dias }}</p><p class="text-center">dias</p>
            </v-col>
            <v-col cols="3">
                <p class="text-center">{{ tiempoRestante.horas }}</p><p class="text-center">horas</p>
            </v-col>
            <v-col cols="3">
                <p class="text-center">{{ tiempoRestante.minutos }}</p><p class="text-center">min</p>
            </v-col>
            <v-col cols="3">
                <p class="text-center">{{ tiempoRestante.segundos }}</p><p class="text-center">seg</p>
            </v-col>
        </v-row>
      </h3>
    </div>
</template>

<script setup>
import evento from "@/mocks/eventos.json";
import { ref, onMounted, onBeforeUnmount, onUpdated } from "vue";

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

onMounted(() => {
  calcularTiempoRestante();
  interval.value = setInterval(calcularTiempoRestante, 1000);
})
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Lobster&display=swap');
.container {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    background-color: beige;
}

h1 {
    font-family: 'Lobster', sans-serif;
    font-size: 10em;
    color: rgb(51, 94, 94);
}

h3 {
    color: rgb(126, 50, 0);
}

@media only screen and (max-width: 1000px) {
    h1 {
        font-size: 5em;
    }
}
</style>