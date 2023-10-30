<script setup>
import HeroVue from './components/Hero/HeroVue.vue'
import CreatorVue from './components/Creator/CreatorVue.vue'
import CardsVue from './components/Cards/CardsVue.vue'
import { onMounted, ref } from 'vue'
import gsap from 'gsap'
import { Observer } from 'gsap/Observer'

gsap.registerPlugin(Observer)

const main = ref(null)
const animating = ref(false)
const mainSlides = ref([])
const slideNumber = ref(0)

const gotoSection = (index) => {
  slideNumber.value = index

  if (window.innerWidth < 750) {
    mainSlides.value.forEach((slide, index) => {
      if (index == slideNumber.value) {
        slide.scrollIntoView({ behavior: 'smooth' })
      }
    })
  } else {
    animating.value = true
    const timeline = gsap.timeline({
      defaults: { duration: 0.6, delay: 0, ease: 'power1.inOut' },
      onComplete: () => {
        animating.value = false
      },
    })

    timeline.to(main.value, { y: `-${slideNumber.value}00%` })

    mainSlides.value.forEach((slide, index) => {
      slide.classList.remove('active-screen')
      if (index == slideNumber.value) {
        slide.classList.add('active-screen')
      }
    })
  }
}

onMounted(() => {
  mainSlides.value = document.querySelectorAll('section')
  if (window.innerWidth > 750) {
    setTimeout(() => {
      Observer.create({
        target: main.value,
        type: 'wheel',
        wheelSpeed: -1,
        onDown: () => {
          if (!animating.value && slideNumber.value !== 0) {
            slideNumber.value--
            gotoSection(slideNumber.value)
          }
        },
        onUp: () => {
          if (!animating.value && slideNumber.value !== mainSlides.value.length - 1) {
            slideNumber.value++
            gotoSection(slideNumber.value)
          }
        },
        tolerance: 10,
        preventDefault: true,
      })
    }, 3000)
  }

  gotoSection(0, 1)
})
</script>

<template>
  <main
    ref="main"
    class="main"
  >
    <HeroVue />
    <CreatorVue :active="slideNumber" />
    <CardsVue :active="slideNumber" />
  </main>
</template>

<style lang="scss" scoped>
.main {
  position: fixed;
  height: 100vh;
  width: 100%;
  transition: all ease-in-out 1s;

  @media (max-width: 750px) {
    position: static;
    height: auto;
  }
}
</style>
