<script setup lang="ts">
type Size = {
  size: string;
  availability: Availability | string;
};

enum Availability {
  InStock = '',
  OutOfStock = 'подписка',
  Limited = 'мало',
}

type Props = {
  sizes: Size[];
};

defineProps<Props>();
</script>

<template>
  <div class="sizes">
    <div class="sizes-title">Размеры</div>
    <div class="sizes-list">
      <div v-for="size in sizes" :key="size.size" class="size">
        <div class="size-name" :class="size.availability === Availability.OutOfStock && 'out-of-stock'">
          {{ size.size }}
        </div>
        <div
          v-if="size.availability !== Availability.InStock"
          :class="{
            'out-of-stock': size.availability === Availability.OutOfStock,
            limited: size.availability === Availability.Limited,
          }"
        >
          {{ size.availability }}
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.sizes-title {
  margin-bottom: 8px;
  color: #4f4f4f;
}

.sizes-list {
  display: flex;
  gap: 14px;
}

.size {
  display: flex;
  flex-direction: column;
  gap: 3px;
  align-items: center;

  .limited {
    color: #828282;
  }

  .out-of-stock {
    color: #bdbdbd;
    border-color: #bdbdbd;
  }
}

.size-name {
  padding: 9px 25px;
  border: 1px solid #333;
}
</style>
