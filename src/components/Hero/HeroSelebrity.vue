<script setup>
import getImageUrl from '../../helpers/getImageUrl'

const props = defineProps({
  selebrity: {
    type: Object,
    default: () => {},
  },
})
</script>
<template>
  <div
    ref="heroSelebrity"
    class="hero-selebrity"
  >
    <div
      class="hero-selebrity__inner"
      :style="{ backgroundImage: `url(${getImageUrl(selebrity.photo)})` }"
    >
      <div class="hero-selebrity__top">
        <h3 class="hero-selebrity__name">
          {{ selebrity.name }}
        </h3>
        <div class="hero-selebrity__subs">
          {{ selebrity.subs }}
        </div>
      </div>
      <div class="hero-selebrity__bot">
        <div class="hero-selebrity__price">
          <div class="hero-selebrity__type">Market price</div>
          <div class="hero-selebrity__value">
            {{ selebrity.price }}
          </div>
        </div>
        <div class="hero-selebrity__time">
          <div class="hero-selebrity__type">remainig time</div>
          <div class="hero-selebrity__value">
            {{ selebrity.time }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style lang="scss" scoped>
.hero-selebrity {
  & + div {
    margin-left: 24px;
  }

  max-width: 271.64px;
  width: 100%;
  height: 325.79px;
  border-radius: 30px;
  overflow: hidden;

  &__inner {
    padding: 24px 28px;
    padding-bottom: 30px;

    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    color: #fff;
    font-family: 'Inter-Medium';
    font-weight: 500;
    font-size: 10px;
    text-transform: uppercase;

    background-position: 0 0;
    background-repeat: no-repeat;
    background-size: cover;
    overflow: hidden;
  }

  &__name {
    font-size: 29px;
    line-height: 38.18px;
    margin-bottom: 6px;
    text-transform: capitalize;
    letter-spacing: 0.8px;
  }

  &__subs {
    letter-spacing: 1px;
  }

  &__bot {
    display: flex;
    justify-content: space-between;
  }

  &__type {
    margin-bottom: 2px;
  }

  &__value {
    font-family: 'Roboto';
    font-weight: 600;
    font-size: 21.69px;
    line-height: 28.2px;
  }

  @media (max-width: 1060px) {
    &:nth-of-type(2) {
      display: none;
    }
  }

  @media (max-width: 920px) {
    &:nth-of-type(4) {
      display: none;
    }
  }

  @media (max-width: 640px) {
    & + div {
      margin-left: 0;
    }
  }
}
</style>
