<script setup>
import SearchIcon from '@/assets/SearchIcon.vue'
import ArrowIcon from '@/assets/ArrowIcon.vue'
import Clouds from '@/assets/Clouds.vue'

const inputCity = defineModel('inputCity')

defineProps({
  weatherInfo: {
    type: [Object, null],
    required: true
  }
})

const capitalizeFirstLatter = (str) => {
  if (!str) {
    return
  }

  return str.charAt(0).toUpperCase() + str.slice(1)
}

const today = new Date().toLocaleString('en-EN', {
  day: 'numeric',
  year: 'numeric',
  month: 'long'
})

const emit = defineEmits(['getCity'])
</script>

<template>
  <section class="w-1/4 bg-white rounded-xl h-full p-6">
    <div class="relative">
      <SearchIcon />
      <input
        type="text"
        v-model="inputCity"
        @keyup.enter="emit('getCity')"
        @focusout="emit('getCity')"
        placeholder="Search city"
        class="bg-inherit border-b border-b-gray-300 outline-0 pl-6 text-sm w-full"
      />
    </div>
    <div class="flex flex-col justify-around h-full">
      <div class="relative">
        <img :src="`/img/${weatherInfo.weather[0].description}.png`" alt="" class="w-52 h-52" />
        <p class="text-9xl font-semibold absolute bottom-16 right-3 opacity-75 text-gray-950">
          <span>{{ Math.round(weatherInfo.main.temp) }}<sup class="ml-2">ͦ</sup></span>
        </p>
        <div class="flex justify-between mt-4">
          <div class="flex items-center">
            <ArrowIcon />
            <p>{{ weatherInfo.main.temp_max }}<sup class="ml-2">ͦ</sup></p>
          </div>
          <div class="flex items-center">
            <ArrowIcon style="rotate: 180deg" />
            <p>{{ weatherInfo.main.temp_min }}<sup class="ml-2">ͦ</sup></p>
          </div>
        </div>
      </div>
      <div class="text-center flex items-center gap-2 justify-center">
        <p>
          <Clouds style="width: 30px" />
        </p>
        <p>{{ capitalizeFirstLatter(weatherInfo.weather[0].description) }}</p>
      </div>
      <div class="text-center relative">
        <p class="mb-1 z-20 text-lg font-bold text-gray-600 block relative">{{ today }}</p>
        <p class="text-sm text-gray-700">{{ weatherInfo.name }}, {{ weatherInfo.sys.country }}</p>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped></style>
