<script setup>
defineProps({
  itemInfo: Object
})
</script>

<template>
  <div class="itemCard bg-white p-5 rounded-xl w-52">
    <p>{{ itemInfo.title }}</p>
    <div v-html="itemInfo.icon"></div>
  </div>
</template>

<style lang="scss" scoped>
.itemCard {
  box-shadow: 0 0 1rem 0 rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(5px);
  background-color: rgb(255 255 255 / 50%);
}
</style>
