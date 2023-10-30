<script setup>
import Card from './CardVue.vue'
import getImageUrl from '../../helpers/getImageUrl'
import { watch, ref } from 'vue'
import gsap from 'gsap'

const props = defineProps({
  active: {
    type: Number,
    default: 0,
  },
})

const cards = [
  {
    image: 'card-1.png',
    title: 'Creators',
    text: 'Creators earn through token sales, engaging with existing fans and drawing in new supporters',
  },
  {
    image: 'card-2.png',
    title: 'Fans',
    text: 'Fans receive regular payments for holding their tokens. Payments are drawn from ad revenue of their favorite social media creators.',
  },
]

const greyCrown = ref(null)
const heart = ref(null)

const startAnimations = () => {
  gsap.to(greyCrown.value, {
    delay: 3.5,
    duration: 15,
    x: '100%',
    y: '-64%',
    ease: 'sine.out',
  })

  gsap.from('.card', {
    delay: 1,
    duration: 2,
    rotate: -90,
    autoAlpha: 0,
    y: 400,
    ease: 'sine.out',
    stagger: { each: 0.3, amount: 1 },
  })

  gsap.fromTo(
    '.card__image',
    {
      x: '40px',
    },
    {
      delay: 2,
      duration: 2,
      x: '-20px',
      ease: 'sine.out',
      stagger: { each: 0.3, amount: 1 },
    },
  )

  gsap.from('.card__title', {
    delay: 2,
    duration: 2,
    y: 15,
    autoAlpha: 0,
    ease: 'sine.out',
  })
  gsap.from('.card__text', {
    delay: 2.3,
    duration: 2,
    y: 15,
    autoAlpha: 0,
    ease: 'sine.out',
  })

}

const removeAnimations = () => {
  gsap.to(greyCrown.value, {
    delay: 3,
    duration: 10,
    x: '0%',
    y: '30%',
    ease: 'sine.out',
  })
}

watch(
  () => props.active,
  () => {
    props.active === 2 && startAnimations()
    props.active === 1 && removeAnimations()
  },
)
</script>
<template>
  <section class="cards">
    <div class="cards__inner">
      <div
        ref="greyCrown"
        class="cards__bg"
      >
        <svg
          class="cards__vector"
          width="938"
          height="1118"
          viewBox="0 0 938 1118"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            class="crown-path"
            d="M496.764 25.769C520.757 59.8775 545.483 92.9276 569.593 126.867C666.784 263.681 759.422 405.268 846.191 555.602C869.864 596.617 891.285 638.825 911.321 682.931C915.092 691.233 913.907 691.964 907.588 685.748C870.976 649.737 834.788 613.194 797.459 579.148C649.981 444.642 498.064 330.151 341.839 237.269C305.3 215.546 267.392 200.405 231.118 177.775C221.746 171.928 246.211 199.629 254.104 209.995C295.922 264.914 338.576 318.304 380.698 372.676C467.067 484.162 547.523 606.476 626.499 728.882C644.626 756.977 672.386 792.46 684.818 826.785C686.857 832.414 682.117 828.526 680.177 827.093C652.543 806.687 625.399 782.687 598.074 761.002C420.269 619.9 241.346 495.598 57.5952 389.792C55.6901 388.695 20.4852 364.549 25.3472 375.742C35.1629 398.34 53.1434 417.882 66.0918 436.371C113.464 504.013 158.249 575.576 202.64 647.154C271.352 757.95 335.607 873.167 401.716 986.832C422.935 1023.31 445.143 1058.76 469.067 1091.55"
            stroke="#F4F4F4"
            stroke-width="50"
            stroke-linecap="round"
          />
        </svg>
      </div>
      <div class="cards__content">
        <Card
          v-for="card in cards"
          :key="card.title"
          :card="card"
        />
      </div>
      <div class="cards__image">
        <svg
          class="cards__heart"
          width="289"
          height="278"
          viewBox="0 0 289 278"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            ref="heart"
            class="heart-path"
            d="M48.501 7.75179C120.428 15.5638 112.053 157.179 112.053 157.179C112.053 157.179 248.048 98.949 278.818 155.208C309.588 211.467 50.619 285.734 42.0561 266.51C7.58891 189.13 -16.0871 0.736847 48.501 7.75179Z"
            stroke="#82FF8E"
            stroke-width="15"
            stroke-linecap="round"
          />
        </svg>
      </div>
    </div>
  </section>
</template>
<style lang="scss" scoped>
.cards {
  &__inner {
    position: relative;
    max-width: 1440px;
    width: 100%;
    margin: 0 auto;
    padding: 0 10px;
  }

  &__content {
    max-width: 1400px;
    width: 100%;
    margin: 0 auto;
    display: flex;
    justify-content: center;
  }

  &__bg,
  &__image {
    position: absolute;
  }

  &__bg {
    transform: translate(100%, -64%);
    z-index: 0;
  }

  &__vector {
    height: 731px;
    transform: scale(1.5);
  }

  &__image {
    right: -5%;
    bottom: -20%;
  }

  @media (max-width: 1170px) {
    &__content {
      flex-direction: column;
      align-items: center;
    }

    &__image {
      display: none;
    }
  }

  @media (max-width: 744px) {
    &__bg {
      display: none;
    }
  }

  .crown-path {
    stroke-dasharray: 4092.055908203125;
    stroke-dashoffset: 4092.055908203125;
    animation: dashCrown 10s linear forwards infinite;
  }

  @keyframes dashCrown {
    from {
      stroke-dashoffset: 4070;
    }
    to {
      stroke-dashoffset: 0;
    }
  }
  .heart-path {
    stroke-dasharray: 921.872802734375;
    stroke-dashoffset: 921.872802734375;
    animation: dashHeart 5s linear forwards;
  }

  @keyframes dashHeart {
    from {
      stroke-dashoffset: 900;
    }
    to {
      stroke-dashoffset: 0;
    }
  }
}
</style>
