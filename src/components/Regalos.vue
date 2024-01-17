<template>
    <div class="container">
        <h1>Regalos</h1>
        <h3 class="text-center mb-5">¿Te gustaría regalarme algo más, aparte de tu maravillosa presencia?</h3>
        <v-dialog width="600">
            <template v-slot:activator="{ props }">
                <v-btn size="x-large" variant="flat" color="#003b6e" v-bind="props" append-icon="mdi-gift">regalos</v-btn>
            </template>
            <template v-slot:default="{ isActive }">
                <v-card style="padding: 5%;">
                    <v-card-text>
                        <Icon icon="teenyicons:gift-outline" height="100" class="icono mt-5" style="display: block; margin: 0 auto;" />
                        <h2>Lo más importante para mí es tu presencia</h2>
                        <h2>pero si deseas hacernme un regalo aquí te
                            dejo los datos</h2>
                        <h2 class="mt-3">CBU: 00000000000000000</h2>
                        <h2>Alias: alias</h2>
                        <h2>titular de la cuenta</h2>
                    </v-card-text>
                    <v-card-actions class="justify-end">
                        <v-btn variant="text" @click="isActive.value = false">cerrar</v-btn>
                    </v-card-actions>
                </v-card>
            </template>
        </v-dialog>
        
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
    background-color: beige;
    padding: 6%;
}

h1 {
    font-family: 'Lobster', sans-serif;
    font-size: 100pt;
    color: rgb(51, 94, 94);
}

h3 {
    color: rgb(126, 50, 0);
    font-size: 30pt;
}

</style>