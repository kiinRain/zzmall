<template>
  <swiper>
    <swiper-item v-for="item in banners.list" :key="item.index">
      <a :href="item.link">
        <img :src="item.image" />
      </a>
    </swiper-item>
  </swiper>
</template>

<script>
import { Swiper, SwiperItem } from "components/common/swiper/index";

export default {
  name: 'HomeSwiper',
  components: {
    Swiper,
    SwiperItem
  },
  props: {
    banners:{
      // type: Array,
      default(){
        return []
      }}
  }
};
</script>

<style>
</style>