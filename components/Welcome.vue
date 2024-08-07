<template>
  <header id="welcome" class="t-welcome relative h-screen flex justify-center items-center">
    <h1 class="text-big1 flex flex-col items-center leading-[1.5]">
      <span :ref="letters[0]">Hello, I'm </span>
      <span class="t-max13h relative flex flex-col items-center leading-[0.9]">
        <span :ref="letters[1]">Maxime</span>
        <span :ref="letters[2]">Hmae</span>
      </span>
    </h1>
    <div class="t-scrolldown absolute bottom-4 left-1/2 -translate-x-1/2 flex flex-col items-center">
      <p>Scroll down !</p>
      <Icon name="fluent:arrow-circle-down-12-filled" size="2rem" class="text-dark"  />
    </div>
  </header>
</template>

<script setup lang="ts">
import { gsap } from "gsap"
import { CustomEase } from "gsap/CustomEase"
import { ScrollTrigger } from "gsap/ScrollTrigger"

const letters = [ref(), ref(), ref()]
const gsapStore = useGsapStore()
const lenisStore = useLenisStore()

onMounted(() => {
  letters.map((el) => {
    splitLettersInHTML(el, 't-helloimmax13h-letters')
  })

  gsap.registerPlugin(CustomEase)
  gsap.registerPlugin(ScrollTrigger)


  gsap.timeline({
    scrollTrigger: {
      trigger: '.t-welcome',
      start: 'bottom 90%',
      end: 'bottom 90%',
      toggleActions: 'play none reverse none',
    }
  })
  .to('.t-helloimmax13h-letters', {
    duration: 1,
    ease: "power4.in",
    yPercent: -200,
    xPercent: (index) => {
      const obj: any = {}
      for (let i = 0; i < 9; i++) {
        const value = -500 + (i * (1000 / 8));
        obj[i] = value;
      }
      for (let i = 0; i < 7; i++) {
        const value = -200 + (i * (400 / 5));
        obj[i + 9] = value;
      }
      return obj[index]
    },
    opacity: 0,
  }, 0)
  .to('.t-scrolldown', {
    duration: 1,
    ease: "power4.in",
    yPercent: -100,
    opacity: 0,
  }, 0)


  gsap.timeline({
    autoRemoveChildren: true,
    delay: 2.5
  })
  .from('.t-helloimmax13h-letters', {
    xPercent: 5000,
    duration: 1,
    stagger: 0.05,
    ease: CustomEase.create("custom", "M0,0 C0.169,0.85 0.054,1.025 1,1 "),
  })
  .to('.t-helloimmax13h-letters', {
    rotate: () => `-${Math.floor(Math.random() * 20  + 10)}`,
    duration: 0.1,
    delay: 0.3,
    stagger: 0.06,
  }, '<')
  .to('.t-helloimmax13h-letters', {
    rotate: () => `${Math.floor(Math.random() * 16 - 8)}`,
    duration: 0.5,
    delay: 0.6,
    stagger: 0.06,
  }, '<')
  .to('.t-max13h', {
    overflow: 'hidden'
  })
  .to('html', {
    '--display-max13h': 'block'
  }, '<')
  .to('html', {
    duration: 0.4,
    '--bottom-max13h': -50
  }, '<')
  .to('.t-max13h', {
    duration: 0.1,
    fontFamily: 'farnhamtext-regularlfregular',
  })
  .to('html', {
    duration: 0.4,
    '--bottom-max13h': 100,
    onComplete: () => {
      gsapStore.isWelcomed = true
      lenisStore.lenis.start()
    }
  }, '<')
  .to('html', {
    '--display-max13h': 'none',
    overflow: 'visible'
  })
  .to('.t-max13h', {
    overflow: 'visible'
  }, '<')
  .from('.t-scrolldown', {
    duration: 1,
    opacity: 0
  }, '<')
  .from('nav', {
    duration: 2,
    opacity: 0,
  }, '<')
})
</script>

<style scoped>
.t-max13h::after {
  content: '';
  position: absolute;
  bottom: var(--bottom-max13h);
  display: var(--display-max13h);
  left: 50%;
  transform: translateX(-50%);
  border-radius: 100%;
  width: calc(10rem + 50vw);
  height: calc(7rem + 50vw);
  @apply bg-light
}

</style>
