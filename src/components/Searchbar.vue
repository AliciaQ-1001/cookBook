<script setup>
import { ref } from "vue";
import searchIcon from "@/assets/images/search.png";
defineProps(["outer-bg", "inner-bg", "has-border"]);
</script>

<template>
  <div class="searchbar-wrapper" :style="{ backgroundColor: outerBg }">
    <div :style="{ backgroundColor: innerBg }" :class="{ border: hasBorder }">
      <img :src="searchIcon" alt="" />
      <span>想吃什么搜这里</span>
    </div>
  </div>
</template>

<style lang="scss">
@import "@/assets/border.scss";
.searchbar-wrapper {
  padding: 10px 15px;
  > div {
    width: 100%;
    height: 40px;
    border-radius: 5px;
    display: flex;
    align-items: center;
    justify-content: center;
    &.border {
      @include border(1px, #db7093, solid, 5px);
    }
    img {
      width: 20px;
    }
    span {
      font-size: 12px;
    }
  }
}
</style>

