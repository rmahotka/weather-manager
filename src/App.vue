<template>
  <main class="main rounded-xl">
    <WeatherSummary />
  </main>
</template>

<script setup>
import { ref } from 'vue'

import WeatherSummary from './components/WeatherSummary.vue'
</script>

<style lang="scss" scoped>
.main {
  width: 1000px;
  height: 500px;
  box-shadow: 0 0 1rem 0 rgba(0, 0, 0, 0.2);
  background-color: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(5px);
}
</style>
