<script setup>
import { onMounted, ref, computed } from 'vue'
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

const sunSet = computed(() => {
  return weatherInfo.value?.sys.sunset
})

const sunRise = computed(() => {
  return weatherInfo.value?.sys.sunrise
})
const wind = computed(() => {
  return `${weatherInfo.value?.wind?.speed} m/sec`
})
const realFeel = computed(() => {
  return `${Math.round(weatherInfo.value?.main?.feels_like)}`
})
const clouds = computed(() => {
  return `${weatherInfo.value?.clouds?.all} %`
})
const visibility = computed(() => {
  return `${weatherInfo.value?.visibility / 1000} km`
})

const objectCard = ref({
  sunSet: {
    icon: `<svg width="95px" height="95px" viewBox="0 0 16 16" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<path fill="#000" d="M10 3h-1v-2h-2v2h-1l2 3 2-3z"></path>
<path fill="#000" d="M14 13l-1.58-1.18 0.78-1.82-2-0.23-0.2-1.97-1.82 0.78-1.18-1.58-1.18 1.58-1.82-0.78-0.23 2-1.97 0.2 0.78 1.82-1.58 1.18h-2v1h16v-1h-2zM4 13c0.075-2.178 1.822-3.925 3.993-4 2.185 0.075 3.932 1.821 4.007 3.993l-8 0.007z"></path>
</svg>`,
    title: 'Sun Set',
    text: sunSet
  },
  sunRise: {
    icon: `<svg width="95px" height="95px" viewBox="0 0 16 16" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<path fill="#000" d="M6 4h1v2h2v-2h1l-2-3-2 3z"></path>
<path fill="#000" d="M12.42 11.82l0.78-1.82-2-0.23-0.2-1.97-1.82 0.78-1.18-1.58-1.18 1.58-1.82-0.78-0.23 2-1.97 0.2 0.78 1.82-1.58 1.18h-2v1h16v-1h-2zM4 13c0.075-2.178 1.822-3.925 3.993-4 2.185 0.075 3.932 1.821 4.007 3.993l-8 0.007z"></path>
</svg>`,
    title: 'Sun Rise',
    text: sunRise
  },
  wind: {
    icon: `<svg class="feather feather-wind" fill="none" height="95" width="95" stroke="#000" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M9.59 4.59A2 2 0 1 1 11 8H2m10.59 11.41A2 2 0 1 0 14 16H2m15.73-8.27A2.5 2.5 0 1 1 19.5 12H2"/></svg>`,
    title: 'Wind',
    text: wind
  },
  realFeel: {
    icon: `<svg viewBox="0 0 256 256" height="95" width="95" xmlns="http://www.w3.org/2000/svg"><rect fill="none" height="95" width="95"/><path d="M96,147V48a32,32,0,0,1,64,0v99h0a52,52,0,1,1-64,0Z" fill="none" stroke="#000" stroke-linecap="round" stroke-linejoin="round" stroke-width="16"/><circle cx="128" cy="188" fill="none" r="20" stroke="#000" stroke-linecap="round" stroke-linejoin="round" stroke-width="16"/><line fill="none" stroke="#000" stroke-linecap="round" stroke-linejoin="round" stroke-width="16" x1="128" x2="128" y1="168" y2="88"/></svg>`,
    title: 'Real Feel',
    text: realFeel
  },
  clouds: {
    icon: `<svg class="bi bi-clouds" fill="currentColor" height="95" viewBox="0 0 16 16" width="95" xmlns="http://www.w3.org/2000/svg"><path d="M16 7.5a2.5 2.5 0 0 1-1.456 2.272 3.513 3.513 0 0 0-.65-.824 1.5 1.5 0 0 0-.789-2.896.5.5 0 0 1-.627-.421 3 3 0 0 0-5.22-1.625 5.587 5.587 0 0 0-1.276.088 4.002 4.002 0 0 1 7.392.91A2.5 2.5 0 0 1 16 7.5z"/><path d="M7 5a4.5 4.5 0 0 1 4.473 4h.027a2.5 2.5 0 0 1 0 5H3a3 3 0 0 1-.247-5.99A4.502 4.502 0 0 1 7 5zm3.5 4.5a3.5 3.5 0 0 0-6.89-.873.5.5 0 0 1-.51.375A2 2 0 1 0 3 13h8.5a1.5 1.5 0 1 0-.376-2.953.5.5 0 0 1-.624-.492V9.5z"/></svg>`,
    title: 'Clouds',
    text: clouds
  },
  visibility: {
    icon: `<svg fill="#000000" height="95px" width="95px" version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
	 viewBox="0 0 449 449" xml:space="preserve">
<g>
	<g>
		<g>
			<path d="M224.1,128.7c-52.8,0-96,43.2-96,96s43.2,96,96,96s96-43.2,96-96S276.9,128.7,224.1,128.7z M224.1,304.7
				c-44,0-80-36-80-80s36-80,80-80s80,36,80,80S268.1,304.7,224.1,304.7z"/>
			<path d="M198.5,168.7c-3.6,1.6-6.4,3.6-8.8,5.2c-3.6,2.4-4.8,7.6-2.4,11.2c1.6,2.4,4,3.6,6.8,3.6c1.6,0,3.2-0.4,4.4-1.2
				c2-1.6,4-2.8,6.4-3.6c4-1.6,6-6.4,4-10.4C207.3,168.7,202.5,166.7,198.5,168.7z"/>
			<path d="M178.5,224.7c0-7.6,2-15.6,6.4-22.8c2-4,0.8-8.8-3.2-10.8s-8.8-0.8-10.8,3.2c-5.2,9.6-8,20.4-8,30.8
				c0,15.2,4.8,28.8,14.4,39.6c1.6,2,4,2.8,6,2.8s3.6-0.8,5.2-2c3.2-2.8,3.6-8,0.8-11.2C182.1,245.9,178.5,235.9,178.5,224.7z"/>
			<path d="M437.3,194.7c-92.4-99.2-172.8-114-212.8-114s-120.4,14.8-212.8,114c-15.6,16.8-15.6,43.2,0,59.6
				c40,42.8,120.8,114,212.8,114c40,0,120.4-14.8,212.8-114C452.9,237.9,452.9,211.5,437.3,194.7z M425.3,243.5
				c-91.2,98.4-170.8,109.2-200.8,109.2c-85.6,0-162.8-68.4-200.8-109.2c-10-10.4-10-27.2,0-38c91.2-98,170.8-108.8,200.8-108.8
				s109.6,10.8,200.8,109.2C435.3,216.3,435.3,233.1,425.3,243.5z"/>
		</g>
	</g>
</g>
</svg>`,
    title: 'Visibility',
    text: visibility
  }
})

onMounted(getWeather)
</script>

<template>
  <main class="main rounded-xl flex">
    <WeatherSummary
      :weatherInfo="weatherInfo"
      v-model:inputCity="locationCity"
      @get-city="getWeather"
    />
    <div class="p-7 grid grid-cols-12 grid-rows-2 justify-items-center gap-y-6 w-3/4">
      <CardInfoWeather
        class="col-span-4"
        v-for="(item, index) in objectCard"
        :key="index"
        :itemInfo="item"
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
