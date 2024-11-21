<script setup>
import OverLayComponte from './components/OverLayComponte.vue'
</script>

<template>
  <img src="@/assets/Images/bg-cafe.jpg" alt="cafe" />
  <OverLayComponte class="overlay" />
</template>

<style scoped>
img {
  width: 100%;
  aspect-ratio: 5/1;
}
.overlay {
  transform: translateY(-10vh);
}
@media screen and (min-width: 1024px) {
  main {
    width: 80%;
  }
}
</style>
