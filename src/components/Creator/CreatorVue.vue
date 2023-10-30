<script setup>
import { watch, ref, onMounted } from 'vue'
import gsap from 'gsap'
import getImageUrl from '../../helpers/getImageUrl'

const coins = new Array(10).fill('coin.svg')

const props = defineProps({
  active: {
    type: Number,
    default: 0,
  },
})

const coinsContainer = ref(null)
const coinsElements = ref(null)
const greenLine = ref(null)

const startAnimations = () => {
  gsap.to('.creator__words-pseudo', {
    duration: 1,
    delay: 1,
    y: '100%',
    ease: 'power1.out',
  })
  gsap.from('.creator__title', {
    duration: 1,
    delay: 1,
    y: '100%',
    ease: 'power1.out',
  })
  gsap.from('.creator__subtitle', {
    duration: 1.5,
    delay: 1.5,
    y: '100%',
    autoAlpha: 0,
    ease: 'power1.out',
  })

  gsap.from(greenLine.value, {
    width: 0,
    delay: 1.5,
    duration: 1,
    ease: 'power1.out',
  })

  gsap.fromTo(
    coinsContainer.value,
    { x: '-100%' },
    { x: '-50%', delay: 1, duration: 2, ease: 'none' },
  )
  const timeline = gsap.timeline()

  coinsElements.value.forEach((item, index) => {
    timeline.from(
      item,
      {
        duration: 20,
        rotation: index % 2 == 0 ? -10 : 10,
        stagger: { each: 1, amount: -1 },
        ease: 'elastic.out( 3, 0.1)',
        delay: 0,
      },
      0,
    )
  })
}

const removeAnimations = () => {
  gsap.fromTo(
    coinsContainer.value,
    {
      x: '-50%',
    },
    {
      x: '300%',
      duration: 5,
      ease: 'expo.out',
      delay: 0.5,
    },
  )
}

watch(
  () => props.active,
  () => {
    props.active === 1 && startAnimations()
    props.active === 2 && removeAnimations()
  },
)
</script>
<template>
  <section class="creator">
    <div class="creator__inner">
      <h2 class="creator__title">
        <div class="creator__words-wrapper">
          <span class="creator__words-pseudo" />Everyone can earn
        </div>
        <div class="creator__words-wrapper">
          <span class="creator__words-pseudo" />
          in the
          <span class="creator__line">
            <span class="creator__text"> new creator </span>
            <img
              ref="greenLine"
              :src="getImageUrl('green-line.svg')"
              class="creator__img"
            />
          </span>
        </div>
        <div class="creator__words-wrapper">
          <span class="creator__words-pseudo" />economy
        </div>
      </h2>
      <div class="creator__subtitle">
        Trade creator on Royalty’s open marketplace platform with ease!
      </div>

      <div
        ref="coinsContainer"
        class="creator-coins"
      >
        <img
          v-for="coin in coins"
          ref="coinsElements"
          :key="coin"
          :src="getImageUrl(coin)"
          alt="coin"
          class="creator-coins__item"
        />
      </div>
    </div>
  </section>
</template>
<style lang="scss" scoped>
.creator {
  &__inner {
    position: relative;
    max-width: 1440px;
    width: 100%;

    min-height: 864px;
    margin: 0 auto;
    padding: 120px 10px 25px 10px;
    overflow-x: hidden;
    z-index: 2;
  }

  &__title {
    max-width: 733px;
    width: 100%;
    margin: 0 auto;
    text-align: center;
    font-size: 80px;
    line-height: 1;
    font-family: 'FKGroteskNeueTrial-Medium';
    font-weight: 500;
    margin-bottom: 25px;
  }

  &__words-wrapper {
    position: relative;
    overflow-y: hidden;
  }

  &__words-pseudo {
    position: absolute;
    height: 100%;
    width: 100%;
    left: 0;
    bottom: 0;
    background-color: #fff;
    z-index: 3;
  }

  &__line {
    position: relative;
  }

  &__text {
    position: relative;
    z-index: 2;
  }

  &__img {
    position: absolute;
    width: 100%;
    top: 50%;
    left: 0;
    transform: translateY(-50%);
  }

  &__subtitle {
    text-align: center;
    font-size: 20px;
    line-height: 25px;
    margin-bottom: 25px;
  }

  @media (max-width: 744px) {
    &__inner {
      padding: 60px 23px 0 23px;
    }

    &__title {
      font-size: 80px;
    }

    &__line {
      display: block;
      width: fit-content;
      margin: 0 auto;
    }
  }

  @media (max-width: 570px) {
    &__inner {
      min-height: 730px;
    }

    &__title {
      font-size: 48px;
      line-height: 1;
    }
  }
}

.creator-coins {
  display: flex;
  align-items: center;
  height: 300px;
  display: flex;
  align-items: center;

  &__item {
    margin-left: -40px;
  }

  @media (max-width: 744px) {
    &__item {
      height: 200px;
    }
  }
}
</style>
