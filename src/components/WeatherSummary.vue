<template>
  <section class="w-1/4 bg-white rounded-xl h-full p-6">
    <div class="relative">
      <svg
        class="absolute top-0 left-0"
        fill="#707070"
        xmlns="http://www.w3.org/2000/svg"
        x="0px"
        y="0px"
        width="20"
        height="20"
        viewBox="0 0 30 30"
      >
        <path
          d="M 13 3 C 7.4889971 3 3 7.4889971 3 13 C 3 18.511003 7.4889971 23 13 23 C 15.396508 23 17.597385 22.148986 19.322266 20.736328 L 25.292969 26.707031 A 1.0001 1.0001 0 1 0 26.707031 25.292969 L 20.736328 19.322266 C 22.148986 17.597385 23 15.396508 23 13 C 23 7.4889971 18.511003 3 13 3 z M 13 5 C 17.430123 5 21 8.5698774 21 13 C 21 17.430123 17.430123 21 13 21 C 8.5698774 21 5 17.430123 5 13 C 5 8.5698774 8.5698774 5 13 5 z"
        ></path>
      </svg>
      <input
        type="text"
        v-model="inputCity"
        @keyup.enter="emit('getCity')"
        placeholder="Search city"
        class="bg-inherit border-b border-b-gray-300 outline-0 pl-6 text-sm w-full"
      />
    </div>
    <div class="flex flex-col justify-around h-full">
      <div class="relative">
        <img src="@/assets/img/weather-main/drizzle.png" alt="" />
        <p class="text-9xl font-semibold absolute bottom-16 right-3 opacity-75 text-gray-950">
          <span>{{ weatherInfo?.main?.temp }}<sup class="ml-2">ͦ</sup></span>
        </p>
        <div class="flex justify-between mt-4">
          <div class="flex items-center">
            <svg
              width="30px"
              height="30px"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M12 5V19M12 5L6 11M12 5L18 11"
                stroke="#000000"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
            <p>32</p>
          </div>
          <div class="flex items-center">
            <svg
              width="30px"
              height="30px"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M12 5V19M12 19L6 13M12 19L18 13"
                stroke="#000000"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
            <p>12</p>
          </div>
        </div>
      </div>
      <div class="text-center flex items-center gap-2 justify-center">
        <p>
          <svg
            width="30px"
            height="30px"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M22 14.3529C22 17.4717 19.4416 20 16.2857 20H11M14.381 9.02721C14.9767 8.81911 15.6178 8.70588 16.2857 8.70588C16.9404 8.70588 17.5693 8.81468 18.1551 9.01498M7.11616 11.6089C6.8475 11.5567 6.56983 11.5294 6.28571 11.5294C3.91878 11.5294 2 13.4256 2 15.7647C2 18.1038 3.91878 20 6.28571 20H7M7.11616 11.6089C6.88706 10.9978 6.7619 10.3369 6.7619 9.64706C6.7619 6.52827 9.32028 4 12.4762 4C15.4159 4 17.8371 6.19371 18.1551 9.01498M7.11616 11.6089C7.68059 11.7184 8.20528 11.9374 8.66667 12.2426M18.1551 9.01498C18.8381 9.24853 19.4623 9.60648 20 10.0614"
              stroke="#1C274C"
              stroke-width="1.5"
              stroke-linecap="round"
            />
          </svg>
        </p>
        <p>Uhundestrorm</p>
      </div>
      <div class="text-center relative">
        <p class="mb-1 z-20 text-lg font-bold text-gray-600 block relative">10 Octouber 2024</p>
        <p class="text-sm text-gray-700">Minsk, Br</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { defineEmits } from 'vue'

const inputCity = defineModel('inputCity')

defineProps({
  weatherInfo: {
    type: [Object, null],
    required: true
  }
})

const emit = defineEmits(['getCity'])
</script>

<style lang="scss" scoped></style>
