<script setup>
import { onMounted, ref } from 'vue'
import WeatherSummary from './components/WeatherSummary.vue'
import CardInfoWeather from './components/CardInfoWeather.vue'

const locationCity = ref('London')
const weatherInfo = ref(null)

const getWeather = async () => {
  try {
    const response = await fetch(
      `${import.meta.env.VITE_API_URL}?APPID=${import.meta.env.VITE_API_KEY}&q=${locationCity.value}&units=metric`
    )
    let data = await response.json()
    weatherInfo.value = data
  } catch (err) {
    console.error(err)
  }
}

const objectCard = {
  sunSet: {
    icon: `
          <svg enable-background="new 0 0 96 96" height="96px" version="1.1" viewBox="0 0 96 96" width="96px" xml:space="preserve" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><g id="Dibujo"><g><path d="M48,30c1.104,0,2-0.896,2-2v-4c0-1.104-0.896-2-2-2c-1.105,0-2,0.896-2,2v4C46,29.104,46.895,30,48,30z"/><path d="M28,46h-4c-1.105,0-2,0.896-2,2s0.895,2,2,2h4c1.104,0,2-0.896,2-2S29.104,46,28,46z"/><path d="M72,46h-4c-1.105,0-2,0.896-2,2s0.895,2,2,2h4c1.104,0,2-0.896,2-2S73.104,46,72,46z"/><path d="M66.385,29.615c-0.781-0.781-2.047-0.781-2.828,0l-2.828,2.828c-0.781,0.781-0.781,2.047,0,2.828    c0.391,0.391,0.902,0.586,1.414,0.586s1.023-0.195,1.414-0.586l2.828-2.828C67.166,31.662,67.166,30.396,66.385,29.615z"/><path d="M35.271,32.443l-2.828-2.828c-0.781-0.781-2.047-0.781-2.828,0c-0.781,0.781-0.781,2.047,0,2.828l2.828,2.828    c0.391,0.391,0.902,0.586,1.414,0.586s1.023-0.195,1.414-0.586C36.053,34.49,36.053,33.225,35.271,32.443z"/><path d="M48,34c-7.72,0-14,6.28-14,14c0,2.449,0.652,4.871,1.888,7.003C36.245,55.62,36.904,56,37.618,56h20.764    c0.714,0,1.373-0.38,1.73-0.997C61.348,52.871,62,50.449,62,48C62,40.28,55.72,34,48,34z M57.157,52H38.843    C38.289,50.738,38,49.375,38,48c0-5.514,4.486-10,10-10c5.514,0,10,4.486,10,10C58,49.375,57.711,50.738,57.157,52z"/><path d="M52.586,64.586L50,67.172V62c0-1.104-0.896-2-2-2c-1.105,0-2,0.896-2,2v5.172l-2.586-2.586    c-0.781-0.781-2.047-0.781-2.828,0c-0.781,0.781-0.781,2.047,0,2.828l6,6C46.977,73.805,47.488,74,48,74    c0.512,0,1.023-0.195,1.414-0.586l6-6c0.781-0.781,0.781-2.047,0-2.828C54.633,63.805,53.367,63.805,52.586,64.586z"/></g></g></svg>
          `,
    title: 'Sun Set',
    text: weatherInfo.value?.sys?.sunset
  }
}

onMounted(getWeather)
</script>

<template>
  <main class="main rounded-xl flex">
    <WeatherSummary
      :weatherInfo="weatherInfo"
      v-model:inputCity="locationCity"
      @get-city="getWeather"
    />
    <div class="p-7 grid grid-cols-12 grid-rows-2 gap-y-6 w-3/4">
      <CardInfoWeather
        class="col-span-4"
        v-for="(item, index) in objectCard"
        :key="index"
        :itemInfo="item"
        :weatherInfo="item.text"
      />
    </div>
  </main>
</template>

<style lang="scss" scoped>
.main {
  width: 1000px;
  height: 500px;
  box-shadow: 0 0 1rem 0 rgba(0, 0, 0, 0.2);
  background-color: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(5px);
}
</style>
