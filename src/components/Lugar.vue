<template>
    <div class="container">
        <h1 class="mb-5">¿Dónde y cuándo?</h1>
      <h3>{{ evento.address }}</h3>
      <h3 class="mb-5">{{ evento.horario }}</h3>
      <v-btn size="x-large" variant="flat" color="#003b6e" append-icon="mdi-send"><a href="https://www.google.com/maps/place/Plaza+Libertad+Santiago+del+Estero/@-27.7938176,-64.2547712,14z/data=!4m6!3m5!1s0x943b52116541bda1:0x63357d1eff4af526!8m2!3d-27.7875278!4d-64.2595019!16s%2Fg%2F1tkkvzln?entry=ttu" target="_blank">Ver en maps</a></v-btn>
    </div>
</template>

<script setup>
import evento from "@/mocks/eventos.json";
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Lobster&display=swap');
.container {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    background-color: rgb(173, 233, 233);
}

h1 {
    font-family: 'Lobster', sans-serif;
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
</style>