<script setup>
import Logo from '~/assets/logo.svg?inline';
import Favorite from '~/assets/favorite.svg?inline';
import User from '~/assets/user.svg?inline';
import Basket from '~/assets/basket.svg?inline';
import Search from '~/assets/search.svg?inline';
</script>

<template>
  <header class="header">
    <div class="icons">
      <div class="mobile-icon">
        <user />
      </div>

      <div class="mobile-icon"><search /></div>
    </div>

    <h1 class="logo-wrapper">
      <logo class="logo" />
      <p style="display: none">stik</p>
    </h1>

    <div class="icons">
      <div class="desktop-icon"><search /></div>
      <div class="desktop-icon">
        <favorite />
      </div>

      <div class="desktop-icon"><user /></div>

      <div><basket /></div>
    </div>
  </header>
</template>

<style scoped>
.header {
  position: relative;

  display: flex;
  align-items: center;
  justify-content: space-between;

  width: 100%;
  height: 50px;
  padding: 0 16px;

  @media screen and (width > 1200px) {
    height: 86px;
    padding: 0 48px;
  }
}

.logo {
  height: 17px;

  @media screen and (width > 1200px) {
    height: 24px;
  }
}

.logo-wrapper {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
}

.icons {
  display: flex;
  gap: 16px;
  align-items: center;

  div {
    cursor: pointer;

    display: flex;
    align-items: center;
    justify-content: center;

    width: 20px;
    height: 20px;
  }
}

.desktop-icon {
  display: none !important;
}

@media screen and (width > 1200px) {
  .mobile-icon {
    display: none !important;
  }

  .desktop-icon {
    display: flex !important;
  }
}
</style>
