<template>
  <div>
    <p class="test inline-block">test</p>
  </div>
</template>

<script setup lang="ts">
import { gsap } from "gsap"

const gsapStore = useGsapStore()

onMounted(() => {
  gsapStore.myProjectsTL = () => {
    return gsap.timeline()
      .to('.test', {
        x: 1000
      })
  }
})
</script>

<style scoped>

</style>
