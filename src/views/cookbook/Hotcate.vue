<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
const hotcate = ref([]);

onMounted(async () => {
  const result = await axios.get("http://localhost:9000/hotcat");
  hotcate.value = [
    ...result.data,
    {
      title: "更多...",
    },
  ];
});
</script>

<template>
  <van-grid :border="false">
    <van-grid-item
      icon="photo-o"
      v-for="hc in hotcate"
      :key="hc.id"
      class="item"
      url="https://www.baidu.com"
    >
      <van-image :src="hc.img" />
      <span>{{ hc.title }}</span>
    </van-grid-item>
  </van-grid>
</template>

<style lang="scss">
.item {
  img {
    width: 60px;
    border-radius: 5px;
  }
  &:last-child {
    .van-icon {
      display: none;
    }
  }
}
</style>
