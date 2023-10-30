<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'
import HeaderVue from '../Header/HeaderVue.vue'
import HeroSelebrity from './HeroSelebrity.vue'

const selebrities = [
  {
    name: 'Monatik',
    photo: 'monatik.png',
    subs: '1 Mil subscribers',
    price: '1,4 RC',
    time: '1Y : 2M : 3H',
  },
  {
    name: 'Diana Show',
    photo: 'diana.png',
    subs: '1 Mil subscribers',
    price: '1,4 RC',
    time: '1Y : 2M : 3H',
  },
  {
    name: 'Anna Trincher',
    photo: 'anna.png',
    subs: '1 Mil subscribers',
    price: '1,4 RC',
    time: '1Y : 2M : 3H',
  },
]

const heroTitle = ref(null)
const heroText = ref(null)
const heroLink = ref(null)

onMounted(() => {
  gsap.from(heroTitle.value.children, {
    delay: 0.5,
    duration: 2.5,
    autoAlpha: 0,
    letterSpacing: 20 + 'px',
    x: 400,
    ease: 'sine.out',
    stagger: 0.3,
  })

  gsap.from('.hero-selebrity', {
    delay: 1,
    duration: 2,
    rotate: -90,
    autoAlpha: 0,
    y: 400,
    ease: 'sine.out',
    stagger: { each: 0.3, amount: -1 },
  })

  gsap.from('.hero-selebrity__inner', {
    delay: 2.1,
    duration: 2.5,
    scale: 1.1,
    ease: 'easy.out',
    stagger: { each: 0.3, amount: -1 },
  })

  gsap.from('.hero-selebrity__top', {
    delay: 2.3,
    duration: 1.5,
    autoAlpha: 0,
    y: 5,
    ease: 'easy.out',
    stagger: { each: 0.3, amount: -1 },
  })

  gsap.from('.hero-selebrity__bot', {
    delay: 2.5,
    duration: 1.5,
    autoAlpha: 0,
    y: 5,
    ease: 'easy.out',
    stagger: { each: 0.3, amount: -1 },
  })

  gsap.from(heroText.value.children, {
    delay: 4,
    duration: 1,
    autoAlpha: 0,
    y: 40,
    ease: 'sine.out',
    stagger: 0.3,
  })

  gsap.from(heroLink.value, {
    delay: 4.5,
    duration: 2.1,
    autoAlpha: 0,
    y: 50,
    ease: 'sine.out',
  })
})
</script>
<template>
  <section class="hero">
    <HeaderVue />
    <div class="hero__inner">
      <div class="hero__star">
        <svg
          width="631"
          height="494"
          viewBox="0 0 631 494"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            ref="starPath"
            class="star-path"
            d="M407.697 180.133C375.895 166.022 311.583 -12.4842 289.674 9.38802C267.766 31.2603 235.256 180.133 214.761 180.133C194.267 180.133 -2.20279 127.216 8.39807 145.561C18.9989 163.905 173.771 282.438 173.065 309.955C172.358 337.472 106.633 484.228 127.128 484.228C147.623 484.228 284.02 357.228 311.583 358.639C339.145 360.05 508.759 500.456 522.186 484.228C535.614 468 447.274 329.711 455.754 309.955C464.235 290.2 646.57 145.561 620.421 145.561C594.272 145.561 439.5 194.244 407.697 180.133Z"
            stroke="#82FF8E"
            stroke-width="15"
            stroke-linecap="round"
          />
        </svg>
      </div>
      <h1
        ref="heroTitle"
        class="hero__title"
      >
        <div>Empowering Every</div>
        <div>Creator Connecting</div>
        <div>Every Fan</div>
      </h1>
      <div class="hero__content">
        <div class="hero__descr">
          <div
            ref="heroText"
            class="hero__text"
          >
            <div>With Royalty, content creators can</div>
            <div>turn ad revenue into digital tokens,</div>
            <div>giving fans the opportunity to</div>
            <div>directly support and invest in their</div>
            <div>favorite creators.</div>
          </div>
          <a
            ref="heroLink"
            href="#"
            class="hero__link"
          >
            Сonnect Wallet
          </a>
        </div>
        <HeroSelebrity
          v-for="selebrity in selebrities"
          :key="selebrity.name"
          :selebrity="selebrity"
        />
      </div>
    </div>
  </section>
</template>
<style lang="scss" scoped>
.hero {
  padding-bottom: 120px;

  &__inner {
    position: relative;
    max-width: 1340px;
    margin: 0 auto;
    padding: 0 10px;
  }

  &__star {
    position: absolute;
    top: 0;
    left: 114px;
    width: 615px;
    height: 478px;
    animation: spin 30s linear 3s infinite;
  }

  &__title {
    position: relative;
    z-index: 2;
    max-width: 863px;
    width: 100%;
    margin-left: auto;
    margin-bottom: 62px;

    font-family: 'FKGroteskNeueTrial-Medium';
    font-weight: 500;
    font-size: 90px;
    line-height: 85.77px;
    white-space: nowrap;
  }

  &__content {
    position: relative;
    z-index: 2;

    display: flex;
    padding-left: 25px;
    padding-bottom: 23px;
  }

  &__descr {
    max-width: 330px;
    width: 100%;
    padding-top: 62px;
    margin-right: 80px;
  }

  &__text {
    font-family: 'FKGroteskNeueTrial-Regular';
    font-size: 20px;
    margin-bottom: 28px;
    line-height: 25.76px;
  }

  &__link {
    font-weight: 600;
    color: #08231e;
    text-transform: uppercase;
    letter-spacing: 2.5px;
    display: block;
  }

  @media (max-width: 920px) {
    &__title {
      font-size: 80px;
      white-space: pre-wrap;
    }
  }

  @media (max-width: 744px) {
    &__inner {
      padding: 0 38px;
    }

    &__content {
      padding-left: 0;
    }

    &__descr {
      margin-right: 40px;
    }
  }

  @media (max-width: 640px) {
    &__title {
      font-size: 48px;
      line-height: 47.76px;
    }

    &__content {
      flex-direction: column;
      align-items: center;
    }

    &__descr {
      order: 1;
      margin-right: 0;
    }
  }

  @media (max-width: 420px) {
    padding-bottom: 60px;

    &__inner {
      padding: 0 23px;
    }

    &__star {
      top: -10%;
      left: -61%;
    }
  }

  .star-path {
    stroke-dasharray: 2150.116455078125;
    stroke-dashoffset: 2150.116455078125;
    animation: dash 5s linear forwards;
  }

  @keyframes dash {
    from {
      stroke-dashoffset: 1600;
    }
    to {
      stroke-dashoffset: 0;
    }
  }

  @keyframes spin {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(180deg);
    }
  }
}
</style>
