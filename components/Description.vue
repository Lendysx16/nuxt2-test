<script setup lang="ts">
import { ref } from 'vue';
import Sizes from './Sizes.vue';
import Favorite from '~/assets/favorite.svg?inline';
import Plus from '~/assets/plus.svg?inline';

type Props = {
  name: string;
  price: number;
};

type Color = {
  name: string;
  color: string;
};

defineProps<Props>();

const sizes = [
  { size: 'XS', availability: 'мало' },
  { size: 'S', availability: '' },
  { size: 'M', availability: 'подписка' },
];

const colors: Color[] = [
  { name: 'Белый', color: '#FFF' },
  { name: 'Черный', color: '#000000' },
  { name: 'Бежевый', color: '#F9F1DC' },
];

const currentColor = ref(0);
</script>

<template>
  <div class="product-description">
    <div class="product-header">
      <div>
        <h3 class="product-name">{{ name }}</h3>
        <p class="product-price">{{ price }} RUB</p>
      </div>

      <Favorite class="mobile-favourite" />
    </div>

    <Sizes :sizes="sizes" class="sizes" />

    <div class="colors">
      <div class="color-name">Цвет: {{ colors[currentColor].name }}</div>

      <div class="colors-list">
        <div
          v-for="(color, index) in colors"
          :key="color.name"
          :class="{ 'color-square': true, 'color-square--selected': currentColor === index }"
          :style="{
            backgroundColor: color.color,
            outlineColor: color.name === 'Белый' ? '#BDBDBD' : 'transparent',
          }"
          @click="currentColor = index"
        />
      </div>
    </div>

    <div class="actions">
      <button class="actions-add">Добавить в корзину</button>
      <button class="actions-save"><Favorite /></button>
    </div>

    <div class="accordions">
      <div class="accordion">
        <h4 class="accordion-title">Описание</h4>
        <span class="accordion-toggle"> <Plus /></span>
      </div>
      <div class="accordion">
        <h4 class="accordion-title">Состав и уход</h4>
        <span class="accordion-toggle"> <Plus /></span>
      </div>
    </div>
  </div>
</template>

<style lang="css" scoped>
.product-header {
  display: flex;
  justify-content: space-between;
}

.product-name,
.product-price {
  margin-bottom: 8px;

  font-size: 12px;
  font-weight: normal;
  line-height: 16px;
  text-transform: uppercase;
}

.mobile-favourite {
  color: #333;
}

.product-price {
  margin-bottom: 36px;
}

.product-description {
  font-size: 10px;
  line-height: 14px;
  color: #333;
}

.colors-list {
  display: flex;
  gap: 16px;
}

.color-square {
  cursor: pointer;

  position: relative;

  width: 28px;
  height: 27px;

  outline: 1px solid transparent;
}

.color-square--selected::after {
  content: '';

  position: absolute;
  bottom: -6px;
  left: 50%;
  transform: translateX(-50%);

  display: block;

  width: 34px;
  height: 1px;

  background-color: #4f4f4f;
}

.color-name {
  margin-bottom: 6px;
  color: #4f4f4f;
}

.colors {
  margin-bottom: 36px;
}

.sizes {
  margin-bottom: 36px;
}

.actions {
  display: none;
  gap: 10px;
  align-items: center;

  width: 100%;
  margin-bottom: 40px;
}

.actions-add {
  flex: 1;

  height: 44px;

  font-size: 11px;
  color: #fff;
  text-transform: uppercase;

  background-color: #000;
  border: none;
}

.actions-save {
  width: 44px;
  height: 44px;

  color: #000;

  background-color: transparent;
  border: 1px solid #000;
}

@media screen and (width > 1200px) {
  .actions {
    display: flex;
  }

  .mobile-favourite {
    display: none;
  }
}

.accordion {
  display: flex;
  align-items: center;
  justify-content: space-between;

  height: 41px;

  border-top: 1px solid #e0e0e0;
}

.accordion:nth-last-child(1) {
  border-bottom: 1px solid #e0e0e0;
}

.accordion-title {
  font-weight: normal;
  color: #333;
  text-transform: uppercase;
}

.accordion-toggle {
  cursor: pointer;
  display: flex;
  align-items: center;
  color: #333;
}
</style>
