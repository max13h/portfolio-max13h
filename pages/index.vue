<template>
  <main class="relative overflow-x-hidden" :class="{ 'overflow-hidden': !gsapStore.isWelcomed }">
    <Entrance v-if="gsapStore.isEntrance" />
    <Navbar />
    <Welcome />
    <section>
      <AboutMeTextPart />
      <AboutMeStackPart />
    </section>
    <MyProjects />
    <Contact />
    <Footer />
  </main>
</template>

<script setup lang="ts">
const gsapStore = useGsapStore()
const lenisStore = useLenisStore()

onMounted(() => {
  const lenis = useLenis()
  lenis.stop()

  lenisStore.lenis = lenis
})
</script>

<style scoped>
</style>
