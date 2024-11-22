<script lang="ts" setup>
import { computed, onMounted, onUnmounted, ref } from 'vue';
import MobilePhotoCarousel from './MobilePhotoCarousel.vue';
import DesktopPhotoCarousel from './DesktopPhotoCarousel.vue';
import Description from './Description.vue';
import ProductSmallCard from './ProductSmallCard.vue';

const photos = ['main.png', 'main-1.png', 'main-2.png'];

const width = ref(Infinity);

const isMobile = computed(() => width.value <= 1200);

function handleResize() {
  width.value = window.innerWidth;
}

onMounted(() => {
  handleResize();
  window.addEventListener('resize', handleResize);
});

onUnmounted(() => {
  window.removeEventListener('resize', handleResize);
});
</script>
<template>
  <div>
    <main class="product">
      <section class="photos">
        <MobilePhotoCarousel v-if="isMobile" :photos="photos" />
        <DesktopPhotoCarousel v-else-if="width !== Infinity" :photos="photos" />
      </section>

      <section class="description">
        <Description :price="8900" name="Жакет удлиненный, белый" />
      </section>
    </main>

    <section class="similar-products">
      <h3 class="simillar-products-title">Похожие товары</h3>
      <div class="similar-products-cards">
        <ProductSmallCard
          imgName="similar.png"
          name="платье с v-образным вырезом, белый"
          :price="14900"
          :last-price="8000"
        />
        <ProductSmallCard imgName="similar-1.png" name="жакет двубортный, серо-голубой" :price="8900" />
        <ProductSmallCard v-if="!isMobile" imgName="similar-2.png" name="платье макси с ярусами, белый" :price="9500" />
        <ProductSmallCard
          v-if="!isMobile"
          imgName="similar-3.png"
          name="комбинезон со стойкой, чёрный"
          :price="10500"
        />
      </div>
    </section>
  </div>
</template>

<style scoped>
.product {
  display: flex;
  flex-direction: column;
  gap: 31px;
  margin: auto;
  margin-bottom: 42px;

  @media screen and (width > 1200px) {
    flex-direction: row;
    gap: 61px;
    width: 78%;
  }
}

.description {
  width: 90%;
  margin: auto;

  @media screen and (width > 1200px) {
    width: 50%;
  }
}

.similar-products {
  width: 90%;
  margin: auto;
  margin-bottom: 200px;

  @media screen and (width > 1200px) {
    width: 100%;
    padding: 0 40px;
    margin-bottom: 100px;
  }
}

.simillar-products-title {
  font-size: 12px;
  line-height: 16px;
  text-transform: uppercase;
  font-weight: normal;
  color: #333;
  margin-bottom: 31px;
}

.similar-products-cards {
  display: grid;
  grid-template-columns: repeat(2, minmax(auto, 1fr));
  gap: 9px;
  width: 100%;

  @media screen and (width > 1200px) {
    grid-template-columns: repeat(4, minmax(auto, 1fr));
  }
}
</style>
