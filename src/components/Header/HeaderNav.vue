<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'
import getImageUrl from '../../helpers/getImageUrl'
const links = ['How it works', 'Creators', 'Holders', 'About us']

const navLinks = ref(null)


onMounted(() => {
  gsap.from(navLinks.value, {
    delay: 0.5,
    duration: 2.5,
    autoAlpha: 0,
    ease: 'sine.out',
    stagger: 0.3,
  })
  
})
</script>
<template>
  <nav class="header-nav">
    <button class="header-nav__menu">
      <img
        :src="getImageUrl('menu-btn.svg')"
        alt="menu button"
        class="header-nav__burger"
      />
    </button>
    <svg
      class="header-nav__frame"
      width="1024"
      height="81"
      viewBox="0 0 1024 81"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <rect
        class="path"
        x="0.5"
        y="0.5"
        width="1023"
        height="80"
        rx="15.5"
        stroke="black"
      />
    </svg>
    <svg
      class="header-nav__frame"
      width="1024"
      height="81"
      viewBox="0 0 1024 81"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <rect
        class="path-next"
        x="0.5"
        y="0.5"
        width="1023"
        height="80"
        rx="15.5"
        stroke-width="1"
        stroke="black"
      />
    </svg>

    <div class="header-nav__icon">
      <img
        :src="getImageUrl('crown.svg')"
        alt="crown"
        class="header-nav__img"
      />
      <img
        :src="getImageUrl('royalty.svg')"
        alt="royalty"
        class="header-nav__img"
      />
    </div>
    <ul class="header-nav__list">
      <li
        v-for="link in links"
        ref="navLinks"
        :key="link"
        class="header-nav__line"
      >
        <a
          href="#"
          class="header-nav__link"
        >
          {{ link }}
        </a>
      </li>
    </ul>
  </nav>
</template>
<style lang="scss" scoped>
.header-nav {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;

  max-width: 1024px;
  width: 100%;
  margin: 0 auto;
  padding: 23px 28px;
  border-radius: 16px;

  &__menu {
    display: none;
    margin-right: 30px;
  }

  &__frame {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 81px;
  }

  &__icon {
    display: flex;
    align-items: center;
  }

  &__img {
    margin-right: 15px;
  }

  &__line {
    display: inline-block;

    & + li {
      margin-left: 40px;
    }
  }

  &__link {
    text-transform: uppercase;
    color: #08231e;
    letter-spacing: 1px;
  }

  @media (max-width: 1060px) {
    justify-content: flex-start;
    border: transparent;

    &__menu {
      display: block;
    }

    &__frame {
      display: none;
    }

    &__list {
      display: none;
    }
  }

  .path {
    stroke-dasharray: 2178.76171875;
    stroke-dashoffset: 2178.76171875;
    animation: dash 4s linear forwards;
  }

  @keyframes dash {
    from {
      stroke-dashoffset: 2000;
    }
    to {
      stroke-dashoffset: 0;
    }
  }

  .path-next {
    stroke-dasharray: 1000;
    stroke-dashoffset: 100;
    animation: dashNext 4s linear forwards;
  }

  @keyframes dashNext {
    from {
      stroke-dashoffset: 0;
    }
    to {
      stroke-dashoffset: 800;
    }
  }
}
</style>
