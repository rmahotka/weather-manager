<template>
  <main class="main rounded-xl">
    <WeatherSummary
      :weatherInfo="resultWeather"
      v-model:inputCity="locationCity"
      @get-city="getWeather"
    />
  </main>
</template>

<script setup>
import { computed, onMounted, ref, watch } from 'vue'
import WeatherSummary from './components/WeatherSummary.vue'

const locationCity = ref('Kobrin')
const resultWeather = ref(null)

const getWeather = async () => {
  try {
    const response = await fetch(
      `https:/${import.meta.env.VITE_API_URL}?APPID=${import.meta.env.VITE_API_KEY}&q=${locationCity.value}&units=metric`
    )
    let data = response.json()
    resultWeather.value = data

    console.log(resultWeather.value)
  } catch (err) {
    console.error(err)
  }
}

watch(resultWeather.value)

onMounted(() => {
  getWeather()
})
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
