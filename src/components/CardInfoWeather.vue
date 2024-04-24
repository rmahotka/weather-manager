<script setup>
defineProps({
  itemInfo: Object
})
</script>

<template>
  <div class="bg-white p-5 rounded-xl w-52 relative">
    <p class="text-gray-800 text-2xl font-bold">{{ itemInfo.title }}</p>
    <p class="text-gray-700 text-lg">{{ itemInfo.text }}</p>
    <div class="opacity-65 absolute bottom-4 right-4" v-html="itemInfo.icon"></div>
  </div>
</template>

<style lang="scss" scoped></style>
