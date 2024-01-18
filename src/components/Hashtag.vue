<template>
  <div class="container">
    <div class="hashtag"></div>
    <Transition name="zoom" mode="out-in">
      <h1 v-if="transitionHashtag" class="text-center">Compartí el momento</h1>
    </Transition>
    <Transition name="fade" mode="out-in">
      <h3 v-if="transitionHashtag" class="mb-5 text-center">
        Subí las fotos con el hashtag
        <strong class="font-weight-black">{{ evento.hashtag }}</strong>
      </h3>
    </Transition>
    <Transition name="slide" mode="out-in">
      <v-btn
        v-if="transitionHashtag"
        size="x-large"
        width="400"
        height="60"
        variant="flat"
        color="#dd7400"
        append-icon="mdi-instagram"
        ><a
          :href="
            'https://www.instagram.com/explore/tags/' +
            evento.hashtag.substring(1)
          "
          target="_blank"
          >ver en instagram</a
        ></v-btn
      ></Transition
    >
  </div>
</template>
  
  <script setup>
import evento from "@/mocks/eventos.json";
import { onMounted } from "vue";
import { ref } from "vue";

const transitionHashtag = ref(false);
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
          transitionHashtag.value = true;
          observer.value.disconnect();
        } else {
          transitionHashtag.value = false;
        }
      });
    };

    observer.value = new IntersectionObserver(handleIntersection, options);

    observer.value.observe(document.querySelector(".hashtag"));
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
  padding: 0 10%;
}

a {
  text-decoration: none;
  color: #ffffff;
}

h1 {
  font-family: "Lobster", sans-serif;
  color: #496074;
  font-size: 50pt;
}

h3 {
  font-size: 25pt;
  color: rgb(97, 97, 97);
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
  transition-delay: calc(0.2s * var(--i));
}

.slide-enter-from,
.slide-leave-to {
  opacity: 0;
  filter: blur(10px);
  transform: translateX(100px);
}

@media only screen and (max-width: 1000px) {
  .container {
    height: 60vh;
  }
}
</style>