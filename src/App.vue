<script setup>
import HomeView from "./views/HomeView.vue";
</script>

<template>
  <HomeView />
  <div class="balloon"></div>
  <div class="balloon"></div>
  <div class="balloon"></div>
  <div class="balloon"></div>
  <div class="balloon"></div>
  <div class="balloon"></div>
  <div class="balloon"></div>
  <div class="balloon"></div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Comfortaa:wght@300&display=swap");

* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  font-family: "Comfortaa", sans-serif;
}

.balloon {
  position: absolute;
  width: 100px;
  height: 110px;
  border-radius: 50%;
  background-color: rgba(192, 1, 5, 0.2);
  animation: move-up 10s infinite;
}
.balloon::before {
  position: absolute;
  content: "";
  width: 1.2px;
  height: 150px;
  background-color: white;
  top: 110px;
  left: 50px;
}
.balloon::after {
  position: absolute;
  content: "";
  border-bottom: 12px solid red;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  top: 109px;
  left: 41px;
}
.balloon:nth-child(2) {
  left: 80%;
  background-color: rgba(11, 11, 226, 0.2);
  animation-duration: 5s;
}
.balloon:nth-child(2)::after {
  border-bottom: 12px solid blue;
}
.balloon:nth-child(3) {
  left: 90%;
  background-color: rgba(253, 253, 4, 0.2);
  animation-duration: 4s;
}
.balloon:nth-child(3)::after {
  border-bottom: 12px solid yellow;
}
.balloon:nth-child(4) {
  left: 70%;
  background-color: rgba(14, 241, 14, 0.2);
  animation-duration: 5s;
}
.balloon:nth-child(4)::after {
  border-bottom: 12px solid green;
}
.balloon:nth-child(5) {
  left: 60%;
  background-color: rgba(184, 6, 9, 0.2);
  animation-duration: 6s;
}
.balloon:nth-child(6) {
  left: 40%;
  background-color: rgba(243, 162, 12, 0.2);
  animation-duration: 5s;
}
.balloon:nth-child(6)::after {
  border-bottom: 12px solid orange;
}
.balloon:nth-child(7) {
  left: 30%;
  background-color: rgba(143, 3, 131, 0.2);
  animation-duration: 7s;
}
.balloon:nth-child(8) {
  left: 20%;
  background-color: rgba(243, 6, 10, 0.2);
  animation-duration: 4s;
}
@keyframes move-up {
  0% {
    top: 100%;
    transform: scale(1);
  }
  50% {
    transform: scale(0.5);
  }
  100% {
    top: -100%;
    transform: scale(1);
  }
}

</style>