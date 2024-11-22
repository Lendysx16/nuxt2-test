<script setup lang="ts">
import { onMounted, ref } from 'vue';

type Props = {
  photos: string[];
};

const { photos } = defineProps<Props>();
const carouselRef = ref<HTMLElement | null>(null);
const currentIndex = ref(0);

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        const img = entry.target.childNodes[0] as HTMLImageElement;

        if (entry.isIntersecting) {
          currentIndex.value = Number(img.dataset.index);
        }
      });
    },
    { threshold: 0.9 },
  );

  if (!carouselRef.value) return;

  carouselRef.value.querySelectorAll('.image-wrapper').forEach((item) => {
    observer.observe(item);
  });
});

function debounce(fn: Function, delay: number) {
  let timer: any;

  return function (...args: any[]) {
    clearTimeout(timer);

    timer = setTimeout(() => {
      fn(...args);
    }, delay);
  };
}

function scroll(event: WheelEvent) {
  if (!carouselRef.value) return;

  if (event.deltaX) {
    carouselRef.value.scrollBy({
      left: 150 * -Math.sign(event.deltaY),
      behavior: 'smooth',
    });

    return;
  }

  carouselRef.value.scrollBy({
    left: 200 * Math.sign(event.deltaY),
    behavior: 'smooth',
  });
}
const debouncedScroll = debounce(scroll, 50);
</script>

<template>
  <div class="wrapper">
    <ul class="carousel" @wheel.stop.prevent="debouncedScroll" ref="carouselRef">
      <li class="image-wrapper" v-for="(photo, index) in photos">
        <img
          :key="index"
          :src="require(`~/assets/images/${photo}`)"
          alt="Обложка"
          draggable="false"
          :data-index="index"
          loading="lazy"
        />
      </li>
    </ul>

    <div class="indexes">
      <span v-for="index in photos.length" :key="index - 1" :class="{ active: index - 1 === currentIndex }" />
    </div>
  </div>
</template>
<style>
.carousel {
  scrollbar-width: none;
  scroll-padding: 0 50px;
  scroll-snap-type: x mandatory;

  position: relative;

  overflow: scroll clip;
  display: flex;

  max-width: 600px;
  height: calc(100svh - 50px);
  margin: auto;

  -ms-overflow-style: none;

  ::-webkit-scrollbar {
    width: 0;
    height: 0;
    background: transparent;
  }

  @media screen and (width > 1200px) {
    max-width: 80%;
    height: calc(100svh - 86px);
  }
}

.image-wrapper {
  scroll-snap-align: center;

  z-index: 10;

  display: flex;
  flex: 1 0 100%;

  height: 100%;

  img {
    height: 100%;
    margin: auto;
    object-fit: contain;
    object-position: top;
  }
}

.wrapper {
  position: relative;
}

.indexes {
  position: absolute;
  z-index: 90;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);

  display: flex;
  gap: 10px;
  justify-content: center;

  span {
    cursor: pointer;

    width: 7px;
    height: 7px;

    opacity: 0.5;
    background-color: #fff;
    border-radius: 50%;

    &.active {
      opacity: 1;
    }
  }
}
</style>
