<template>
  <div class="container">
    <div class="confirmacion"></div>
    <Transition name="zoom" mode="out-in">
      <h1 v-if="transitionConfirmacion" class="mb-5 text-center">
        Confirmar asistencia
      </h1>
    </Transition>
    <Transition name="fade" mode="out-in">
      <div v-if="transitionConfirmacion">
        <h3 class="mb-5 text-center">
          Enviá un mensaje a mis papis para confirmar que vas a mi fiesta
        </h3>
      </div>
    </Transition>
    <Transition name="slide" mode="out-in">
      <v-btn
        v-if="transitionConfirmacion"
        size="x-large"
        width="400"
        height="60"
        variant="flat"
        color="#003b6e"
        append-icon="mdi-whatsapp"
        ><a
          :href="
            'https://api.whatsapp.com/send?phone=' +
            evento.whatsapp +
            '&text=Hola!%20Confirmo%20mi%20presencia%20para%20la%20fiesta!%F0%9F%A5%B3'
          "
          target="_blank"
          >whatsapp</a
        ></v-btn
      >
    </Transition>
  </div>
</template>
  
  <script setup>
import evento from "@/mocks/eventos.json";
import { ref, onMounted } from "vue";

const transitionConfirmacion = ref(false);

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
          transitionConfirmacion.value = true;
          observer.value.disconnect();
        } else {
          transitionConfirmacion.value = false;
        }
      });
    };

    observer.value = new IntersectionObserver(handleIntersection, options);

    observer.value.observe(document.querySelector(".confirmacion"));
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
  background-color: rgb(173, 233, 233);
  padding: 0 10%;
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