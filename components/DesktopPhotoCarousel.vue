<script setup lang="ts">
import { ref } from 'vue';

type Props = {
  photos: string[];
};

defineProps<Props>();

const selectedPhoto = ref(0);
</script>
<template>
  <div class="desktop-photos">
    <div class="all-photos">
      <img
        v-for="(photo, index) in photos"
        :key="photo"
        :src="require(`~/assets/images/${photo}`)"
        :class="{
          'image-sm': true,
          'image-sm--selected': index === selectedPhoto,
        }"
        alt="photo"
        @click="selectedPhoto = index"
      />
    </div>
    <div class="selected-photo">
      <img :src="require(`~/assets/images/${photos[selectedPhoto]}`)" alt="photo" class="image-lg" />
    </div>
  </div>
</template>

<style scoped>
.desktop-photos {
  display: flex;
  gap: 30px;
}

.all-photos {
  display: flex;
  flex: 1;
  flex-direction: column;
  gap: 4px;
}

.image-sm {
  width: 70px;
  height: 87px;

  opacity: 1;
  object-fit: cover;

  transition: opacity 0.3s;

  &:hover {
    cursor: pointer;
    opacity: 0.5;
  }
}

.image-sm--selected {
  opacity: 0.5;
}

.selected-photo {
  width: 520px;
  height: 693px;
}

.image-lg {
  display: block;

  width: 100%;
  height: 100%;

  object-fit: cover;
  object-position: top;
}
</style>
