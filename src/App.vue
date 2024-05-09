<script setup>
import { onMounted, ref, computed } from 'vue'
import WeatherSummary from './components/WeatherSummary.vue'
import CardInfoWeather from './components/CardInfoWeather.vue'
import SunRiseSvg from './assets/SunRise.vue'
import SunSetSvg from './assets/SunSet.vue'
import WindSvg from './assets/Wind.vue'
import RealFeelSvg from './assets/RealFeel.vue'
import CloudsSvg from './assets/Clouds.vue'
import VisabilitySvg from './assets/Visability.vue'

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

function checkInfoText(value, ending = '') {
  if (value) {
    return `${value} ${ending}`
  }
}

const sunSet = computed(() => {
  if (weatherInfo.value.sys.sunset) {
    return new Date(weatherInfo.value.sys.sunset * 1000).toLocaleTimeString('ru-Ru')
  } else {
    return 'н/д'
  }
})

const sunRise = computed(() => {
  if (weatherInfo.value.sys.sunrise) {
    return new Date(weatherInfo.value.sys.sunrise * 1000).toLocaleTimeString('ru-RU')
  } else {
    return 'н/д'
  }
})

const wind = computed(() => {
  return checkInfoText(weatherInfo.value.wind.speed, 'm/sec')
})

const realFeel = computed(() => {
  return checkInfoText(Math.round(weatherInfo.value.main.feels_like))
})

const clouds = computed(() => {
  return checkInfoText(weatherInfo.value.clouds.all, '%')
})

const visibility = computed(() => {
  return checkInfoText(weatherInfo.value.visibility / 1000, 'km')
})

const objectCard = ref({
  sunRise: {
    icon: SunRiseSvg,
    title: 'Sun Rise',
    text: sunRise
  },
  sunSet: {
    icon: SunSetSvg,
    title: 'Sun Set',
    text: sunSet
  },
  wind: {
    icon: WindSvg,
    title: 'Wind',
    text: wind
  },
  realFeel: {
    icon: RealFeelSvg,
    title: 'Real Feel',
    text: realFeel
  },
  clouds: {
    icon: CloudsSvg,
    title: 'Clouds',
    text: clouds
  },
  visibility: {
    icon: VisabilitySvg,
    title: 'Visibility',
    text: visibility
  }
})

onMounted(getWeather)
</script>

<template>
  <main class="main rounded-xl">
    <div v-if="weatherInfo?.cod == 200" class="flex h-full">
      <WeatherSummary
        :weatherInfo="weatherInfo"
        v-model:inputCity="locationCity"
        @get-city="getWeather"
      />
      <div class="p-7 grid grid-cols-12 grid-rows-2 justify-items-center gap-y-6 w-3/4">
        <CardInfoWeather
          v-for="(item, index) in objectCard"
          :key="index"
          :itemInfo="item"
          class="col-span-4"
        />
      </div>
    </div>
    <div class="bg-white h-full rounded-xl p-10" v-else>
      <input
        class="w-full p-1 border-b border-gray-800 text-center outline-none"
        type="text"
        name="ErrorSearch"
        id="ErrorSearch"
        v-model="locationCity"
        @keyup.enter="getWeather"
        placeholder="Search City"
      />
      <div class="flex items-center justify-center h-full">
        <h1 class="text-6xl font-bold text-gray-700">{{ weatherInfo?.message }}</h1>
      </div>
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
