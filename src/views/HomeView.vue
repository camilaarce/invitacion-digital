<template>
  <div class="container">
    <CuentaRegresiva class="items" />
    <Lugar class="items" />
    <Fotos class="items" />
    <Regalos class="items" />
    <Confirmar class="items" />
    <Hashtag class="items" />
  </div>
  <Musica class="music" />
</template>

<script setup>
import Confirmar from "@/components/Confirmar.vue";
import CuentaRegresiva from "@/components/CuentaRegresiva.vue";
import Fotos from "@/components/Fotos.vue";
import Hashtag from "@/components/Hashtag.vue";
import Lugar from "@/components/Lugar.vue";
import Regalos from "@/components/Regalos.vue";
import Musica from "@/components/Musica.vue";
</script>

<style scoped>
.container {
  max-height: 100vh;
  scroll-snap-type: y mandatory;
  overflow-y: scroll;
  position: relative;
}

.music {
  position: absolute;
  top: 1%;
  right: 1%;
}

.items {
  scroll-snap-align: start;
}

*::-webkit-scrollbar {
  width: 0px;
}
</style>
