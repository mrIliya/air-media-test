<script setup>
import { ref } from 'vue'
import gsap from 'gsap'
import getImageUrl from '../../helpers/getImageUrl'

const props = defineProps({
  card: {
    type: Object,
    default: () => {},
  },
})

const link = ref(null)
const cardContainer = ref(null)
const cardImage = ref(null)

const nandleLink = (e) => {
  const x = e.clientX
  const y = e.clientY

  const newposX = x
  const newposY = y

  link.value.style.left = newposX - cardContainer.value.offsetLeft - 340 + 'px'
  link.value.style.top = newposY - cardContainer.value.offsetTop - 380 + 'px'

  cardImage.value.style.top = (y * -1) / 40 + 'px'
  cardImage.value.style.left = (x * -1) / 40 + 'px'
}
</script>
<template>
  <div
    ref="cardContainer"
    class="card"
    @mousemove="(e) => nandleLink(e)"
  >
    <div class="card__inner">
      <a
        ref="link"
        href="#"
        class="card__link"
      >
        Learn more
      </a>
      <div class="card__bg">
        <img
          ref="cardImage"
          class="card__image"
          :src="getImageUrl(card.image)"
          alt="people"
        />
      </div>
      <h3 class="card__title">{{ card.title }}</h3>
      <p class="card__text">{{ card.text }}</p>
    </div>
  </div>
</template>
<style lang="scss" scoped>
.card {
  display: block;
  max-width: 504px;
  width: 100%;
  height: 624px;
  position: relative;
  cursor: none;

  &:hover {
    .card__link {
      opacity: 1;
      z-index: 4;
    }
  }

  &:nth-of-type(1) {
    transform: rotate(-4.72deg);
    margin-right: 104px;
    margin-top: -14px;
    margin-left: 10px;
  }
  
  &:nth-of-type(2) {
    transform: rotate(3.68deg);
    margin-top: 65px;
  }

  &__inner {
    position: relative;
    width: 100%;
    height: 100%;
    padding: 47px;
    padding-bottom: 58px;
    overflow: hidden;

    display: flex;
    flex-direction: column;
    justify-content: flex-end;

    color: #fff;
    border-radius: 38px;
    font-family: 'FKGroteskNeueTrial-Medium';
    font-weight: 500;
  }

  &__link {
    width: 139px;
    height: 139px;

    display: flex;
    align-items: center;
    justify-content: center;

    font-family: 'FKGroteskNeueTrial-Medium';
    font-size: 20px;
    font-weight: 500;
    color: #08231e;

    opacity: 0;
    border-radius: 50%;
    background-color: #82ff8e;
    text-transform: uppercase;
    position: relative;
    z-index: 2;
    cursor: none;

    &:hover {
      opacity: 1;
    }
  }

  &__bg {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    height: 743px;
    width: 1136px;
  }

  &__image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    max-width: none;
    position: relative;
  }

  &__title {
    position: relative;
    z-index: 2;
    font-size: 83px;
    line-height: 80px;
    margin-bottom: 8px;
  }

  &__text {
    position: relative;
    z-index: 2;
    font-weight: 400;
    font-size: 20px;
    line-height: 28px;
  }

  @media (max-width: 1170px) {
    &:nth-of-type(1) {
      transform: rotate(0deg);
      margin: 0 0 48px 0;
    }
    &:nth-of-type(2) {
      transform: rotate(0deg);
      margin-top: 0;
    }
  }

  @media (max-width: 744px) {
    max-width: 618px;
    height: 610px;

    &__link {
      position: absolute;
      right: 47px;
      bottom: 49px;
      z-index: 5;
      visibility: visible;
    }
  }

  @media (max-width: 570px) {
    &__inner {
      text-align: center;
      padding-bottom: 100px;
    }

    &__title {
      font-size: 48px;
      line-height: 1;
    }

    &__text {
      font-size: 14px;
    }

    &__link {
      border-radius: 12px;
      height: 69px;
      max-width: 239px;
      width: 100%;

      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      font-size: 16px;
    }
  }
}
</style>
