<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import swiper1 from "@/assets/images/swiper-1.png";
import swiper2 from "@/assets/images/swiper-2.jpeg";
import swiper3 from "@/assets/images/swiper-3.jpeg";
const list = ref([]);
onMounted(async () => {
  const result = await axios.get("http://localhost:9000/list");
  list.value = result.data.data.slice(0, 5);
});
</script>

<template>
  <div class="swiper-container">
    <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
      <van-swipe-item v-for="li in list" :key="li.id">
        <img :src="li.img" alt="li.name" />
      </van-swipe-item>
    </van-swipe>
  </div>
</template>

<style lang="scss">
.swiper-container {
  height: 0;
  font-size: 0;
  padding-bottom: 66.6666667%;
}
.my-swipe .van-swipe-item {
  img {
    width: 100%;
  }
}
</style>

