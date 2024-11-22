<script setup lang="ts">
type Props = {
  imgName: string;
  name: string;
  price: number;
  lastPrice?: number;
};

defineProps<Props>();
</script>

<template>
  <div class="product-small-card">
    <img :src="require(`~/assets/images/${imgName}`)" alt="product" class="product-small-card__image" />

    <div class="product-small-card-description">
      <h4 class="product-small-card-name">{{ name }}</h4>

      <p>
        <span class="product-small-card-price">{{ price }} RUB</span>
        <span v-if="lastPrice" class="product-small-card-last-price">{{ lastPrice }} RUB</span>
      </p>
    </div>
  </div>
</template>

<style scoped>
.product-small-card {
  display: flex;
  flex-direction: column;
  gap: 15px;

  img {
    width: 100%;
    object-fit: contain;
  }
}

.product-small-card-description {
  max-width: 80%;
  padding-left: 7px;
  font-size: 10px;
  font-weight: normal;

  @media screen and (width > 1200px) {
    max-width: 100%;
    padding-left: 15px;
  }
}

.product-small-card-name {
  margin-bottom: 10px;
  font-size: 10px;
  font-weight: normal;
  text-transform: uppercase;

  @media screen and (width > 1200px) {
    text-transform: none;
  }
}

.product-small-card-last-price {
  color: #828282;
  text-decoration: line-through;
}

.product-small-card-price {
  margin-right: 10px;
  color: #828282;

  @media screen and (width > 1200px) {
    color: #333;
  }
}
</style>
