<template>
  <v-btn
    @click="startAudio"
    color="teal-accent-4"
    :icon="!play ? 'mdi-music' : 'mdi-music-off'"
  ></v-btn>
</template>
  
<script setup>
import { Howl, Howler } from "howler";
import { ref } from "vue";
import musica from "../../public/assets/music/felizcumple.mp3";

const play = ref(false);
let sound = null;

const startAudio = () => {
  play.value = !play.value;

  if (!sound) {
    // Si sound no está definido, crea una nueva instancia
    sound = new Howl({
      src: [musica],
      autoplay: true,
      loop: true,
      volume: 1,
    });

    // Asegúrate de que el audio esté habilitado para reproducirse en el navegador
    Howler.autoUnlock = true;
  }

  if (play.value) {
    sound.play();
  } else {
    sound.pause();
  }
};
</script>

<style scoped>
.v-btn {
  width: 3vw;
  min-width: 50px;
  height: auto;
  aspect-ratio: 1/1;
}
</style>