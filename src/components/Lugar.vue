<template>
    <div class="container">
        <h1>¿Dónde y cuándo?</h1>
      <h3>{{ evento.address }}</h3>
      <h3>{{ evento.horario }}</h3>
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
</style>