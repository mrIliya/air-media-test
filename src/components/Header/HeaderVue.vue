<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'

import HeaderNav from './HeaderNav.vue'

const headerBtn = ref(null)



onMounted(() => {
  gsap.from(headerBtn.value, {
    delay: 0.3,
    duration: 1,
    y: 25,
    autoAlpha: 0.1,
    ease: 'sine.out',
  })

})
</script>
<template>
  <header class="header">
    <div class="header__inner">
      <HeaderNav />
      <button
        ref="headerBtn"
        class="header__btn"
        type="button"
      >
        Launch platform
      </button>
    </div>
  </header>
</template>
<style lang="scss" scoped>
.header {
  padding: 42px 0 70px 0;

  &__inner {
    display: flex;
    align-items: center;
    max-width: 1300px;
    margin: 0 auto;
    padding: 0 10px;
  }

  &__btn {
    display: flex;
    align-items: center;
    justify-content: center;

    max-width: 232px;
    height: 81px;
    width: 100%;
    margin-left: 16px;

    flex: 0 0 auto;
    background-color: #000;
    color: #fff;
    text-transform: uppercase;
    font-weight: 500;
    letter-spacing: 2.5px;
    border-radius: 16px;
  }

  @media (max-width: 1060px) {
    &__btn {
      display: none;
    }
  }
}
</style>
