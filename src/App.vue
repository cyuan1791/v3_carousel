<script setup>

// If you are using PurgeCSS, make sure to whitelist the carousel CSS classes
import 'vue3-carousel/carousel.css'
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'

const carouselConfig = JSON.parse(atob(window.asoneConfig));

let dataHTML = JSON.parse(atob(window.asoneDataHTML));

let useNav = true;
let usePagination = true;

if ("vueOpts" in carouselConfig) {
  if ("useNav" in carouselConfig.vueOpts) {
    useNav = carouselConfig.vueOpts.useNav;
  }
  if ("usePagination" in carouselConfig.vueOpts) {
    usePagination = carouselConfig.vueOpts.usePagination;
  }
}
</script>

<template>
  <Carousel v-bind="carouselConfig">
    <Slide v-for="data in dataHTML" :key="data">
      <div class="carousel__item">

        <div v-html="data['html']"></div>
      </div>
    </Slide>

    <template #addons>
      <Navigation v-if="useNav" />
      <Pagination v-if="usePagination" />
    </template>
  </Carousel>
</template>