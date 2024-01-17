<template>
  <div class="container">
     <CuentaRegresiva class="items" />
      <Lugar class="items" />
      <Fotos class="items" />
  </div>
 
</template>

<script setup>
import CuentaRegresiva from '@/components/CuentaRegresiva.vue';
import Fotos from '@/components/Fotos.vue';
import Lugar from '@/components/Lugar.vue';
</script>

<style scoped>
.container {
  max-height: 100vh;
  scroll-snap-type: y mandatory;
  overflow-y: scroll;
}

.items {
  scroll-snap-align: start;
}

*::-webkit-scrollbar {
  width: 0px;
}
</style>
