<script setup>
defineProps({
  itemInfo: Object,
  weatherInfo: Object
})
</script>

<template>
  <div class="bg-white p-5 rounded-xl w-52">
    <p>{{ itemInfo.title }}</p>
    <div v-html="itemInfo.icon"></div>
    <p>{{ itemInfo.text }}</p>
  </div>
</template>

<style lang="scss" scoped></style>
