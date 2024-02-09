<template>
  <nav class="fixed w-full flex justify-end items-center mix-blend-difference font-light text-light z-50 ">
    <NuxtLink class="transition-all duration-15000 hover:scale-105 hover:outline hover:outline-2 hover:outline-gray-400 py-2 px-4 rounded-2xl mt-4 me-4" @click="lenisStore.lenis.scrollTo('#Contact')">
      Contact
    </NuxtLink>
  </nav>
</template>

<script setup lang="ts">
const lenisStore = useLenisStore()
</script>

<style scoped>
</style>
