<template>
  <div>
    <div class="divider-block-md bg-dark"></div>
    <div class="t-heading relative leading-none">
      <h2 class="
      ms-4
        text-big2
        mix-blend-difference
        text-light
        font-medium
      ">
        Discover my
        <br>
        projects
      </h2>
    </div>

    <div
      class="
        flex
        flex-col
        items-center
        sm:items-start
        sm:flex-row
        sm:flex-nowrap
        sm:overflow-x-scroll
        p-4
      "
    >
      <div
        v-for="(project, index) in projects"
        :key="index"
        class="
          relative
          w-[90vw]
          h-[90vw]
          mt-4
          overflow-hidden
          rounded-2xl
          group
          sm:min-w-[90vw]
          sm:h-[90vw]
          md:min-w-[80vh]
          md:h-[80vh]


          sm:me-8
          sm:last:me-0
          sm:mt-0
        "
        @click="openModal(project.name)"
      >
        <NuxtImg
          :src="project.mainImage"
          class="
            w-[150%]
            transition-all
            blur-sm
            group-hover:blur-[2px]
            group-hover:scale-105
        "/>
        <div class="transition-all group-hover:bg-zinc-900 w-full h-full bg-dark absolute top-0 left-0 opacity-50"></div>
        <h3 class="transition-all group-hover:scale-105   absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 text-big5 text-light w-full text-center">{{ project.name }}</h3>

        <TransitionRoot appear :show="modalOpened === project.name">
          <Dialog @close="closeModal" class="relative z-[400]">
            <TransitionChild
              as="div"
              enter="duration-300 ease-out"
              enter-from="opacity-0"
              enter-to="opacity-100"
              leave="duration-200 ease-in"
              leave-from="opacity-100"
              leave-to="opacity-0"
            >
              <div class="fixed inset-0 bg-light/50" />
            </TransitionChild>

            <div class="fixed inset-0 overflow-y-auto">
              <div
                class="flex min-h-full items-center justify-center p-4"
              >
                <TransitionChild
                  as="div"
                  enter="duration-300 ease-out"
                  enter-from="opacity-0 scale-95"
                  enter-to="opacity-100 scale-100"
                  leave="duration-200 ease-in"
                  leave-from="opacity-100 scale-100"
                  leave-to="opacity-0 scale-95"
                >
                  <DialogPanel class="bg-dark rounded-2xl h-[90vh] w-[90vw] shadow-2xl shadow-dark/50 overflow-y-scroll flex flex-col">
                    <div class="flex-grow p-8 flex flex-col">
                      <h3 class="text-light text-big3">{{ project.name }}</h3>
                      <p class="text-light">{{ project.description }}</p>
                      <NuxtLink :to="project.link" target="_blank" class="bg-gray-300 text-dark px-4 py-2 rounded-3xl w-fit mt-4">
                        {{ project.textLink }}
                      </NuxtLink>
                    </div>
                    <p v-if="project.images.length > 1" class="text-light w-full text-center">
                      Scroll
                      <Icon name="fluent:arrow-right-12-regular" class="filter-light" />
                    </p>
                    <div ref="scroll" class="flex p-4" :class="{'overflow-x-scroll' : project.images.length > 1 }">
                      <NuxtImg v-for="(image, imgIndex) in project.images" :key="imgIndex" :src="project.images[imgIndex]" class="mx-4 first:mx-0 rounded-3xl" />
                    </div>
                  </DialogPanel>
                </TransitionChild>
              </div>
            </div>
          </Dialog>
        </TransitionRoot>
      </div>
    </div>

  </div>
</template>

<script setup lang="ts">
import { gsap } from "gsap"
import { TransitionRoot, TransitionChild, Dialog, DialogPanel, DialogTitle, DialogDescription } from '@headlessui/vue'

const projects = [
  {
    name: 'The Favorite',
    mainImage: 'https://raw.githubusercontent.com/max13h/the_favorite/master/app/assets/images/readme/competition.png',
    description: "The Favorite was my first team project. I led the development of the mobile web app in one month",
    images: [
      "https://raw.githubusercontent.com/max13h/the_favorite/master/app/assets/images/readme/root.png",
      "https://raw.githubusercontent.com/max13h/the_favorite/master/app/assets/images/readme/home_tasks.png",
      "https://raw.githubusercontent.com/max13h/the_favorite/master/app/assets/images/readme/home_events.png",
      "https://raw.githubusercontent.com/max13h/the_favorite/master/app/assets/images/readme/competition.png",
      "https://raw.githubusercontent.com/max13h/the_favorite/master/app/assets/images/readme/common_pot.png",
      "https://raw.githubusercontent.com/max13h/the_favorite/master/app/assets/images/readme/kids.png",
    ],
    link: 'https://github.com/max13h/the_favorite',
    textLink: 'Check the repo'
  },
  {
    name: 'Early stage project',
    mainImage: 'logo_secretproject.png',
    description: '',
    images: ["logo_secretproject.png"],
    link: ''
  },
  {
    name: 'Portfolio',
    mainImage: 'https://raw.githubusercontent.com/max13h/the_favorite/master/app/assets/images/readme/competition.png',
    description: '',
    images: [],
    link: ''
  }
]

const modalOpened = ref('')
function closeModal() {
  modalOpened.value = ''
}
function openModal(technologie: string) {
  modalOpened.value = technologie
}

onMounted(() => {


  // gsap.timeline()
  //   .to('.test', {
  //     x: 1000
  //   })
})

</script>

<style scoped>
.t-heading:after {
  content: '';
  @apply bg-dark absolute top-0 left-0 rounded-b-3xl w-full h-[26%] -z-10
}
</style>
