<script setup>
defineProps({
  itemInfo: Object
})
</script>

<template>
  <div class="bg-white p-5 rounded-xl w-52 relative">
    <p class="text-gray-800 text-2xl font-bold">{{ itemInfo.title }}</p>
    <p class="text-gray-700 text-lg">{{ itemInfo.text }}</p>
    <component :is="itemInfo.icon" class="opacity-65 absolute bottom-4 right-4"></component>
  </div>
</template>

<style lang="scss" scoped></style>
