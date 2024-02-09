<template>
  <div class="relative overflow-x-hidden">
    <Entrance v-if="gsapStore.isEntrance" />
    <Navbar />
    <Welcome />
    <AboutMe />
    <div>
      lorem1000
    </div>
    <!-- <MyProjects /> -->
  </div>
</template>

<script setup lang="ts">
const gsapStore = useGsapStore()

onMounted(() => {
  watchEffect(() => {
    if(gsapStore.isWelcomed) {
      const lenis = useLenis()
    }
  })
})
</script>

<style scoped>
</style>
