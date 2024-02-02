<template>
  <div class="w-full h-screen overflow-hidden flex justify-center items-center">
    <h1 class="main-heading w-full text-center inline-block">
        <span :ref="letters[0]" class="overflow-hidden">Hello,</span>
        <span class="flex flex-wrap justify-center">
          <span :ref="letters[1]" class="me-12 overflow-hidden">I'm </span>
          <span :ref="letters[2]" class="overflow-hidden">max13h</span>
        </span>
    </h1>
  </div>
</template>

<script setup lang="ts">
const letters = [ref(), ref(), ref()]

onMounted(() => {
  letters.map((el, index) => {
    el.value.focus
    el.value.innerHTML = el.value.textContent.replace(/\S/g, `<span class='letter inline-block ${index === 2 ? 'max13h' : ''}'>$&</span>`);
  })
  const { gsap } = useGsapStore()
  const { isEntrance } = storeToRefs(useGsapStore())

  watch(isEntrance, () => {
    if(!isEntrance.value) {
    gsap.timeline()
      .from('.letter', {
        yPercent: 100,
        duration: 0.3,
        stagger: 0.06
      })
      .from('.letter', {
        opacity: 0,
        duration: 0.3,
        stagger: 0.06
      }, '<0.2')
      .to('.letter', {
        rotate: () => `+=${useAnime.random(-8, 8)}`,
        duration: 3,
      }, '-=1')
  }
  })
})
</script>

<style scoped>
.main-heading {
  position: relative;
}

.main-heading .letter {
  display: inline-block;
}
</style>
