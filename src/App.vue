<script setup>
import { ref, watch, onMounted } from "vue";
import { useRoute } from "vue-router";
import useListStore from "@/store/listStore";
import cookbook from "@/assets/images/cookbook.png";
import cookbookActive from "@/assets/images/cookbook-active.png";
import menu from "@/assets/images/menu.png";
import menuActive from "@/assets/images/menu-active.png";
import more from "@/assets/images/more.png";
import moreActive from "@/assets/images/more-active.png";

const active = ref(0);
const title = ref("");
const route = useRoute();
//根据页面的不同改变标题
watch(
  () => route.meta,
  (meta) => {
    title.value = meta.title;
  }
);

const listStore = useListStore();

onMounted(async () => {
  listStore.loadData();
});
</script>

<template>
  <div>
    <van-nav-bar :title="title" safe-area-inset-top />
    <main>
      <router-view></router-view>
    </main>
    <van-tabbar
      v-model="active"
      active-color="#000"
      inactive-color="#ccc"
      route
      safe-area-inset-buttom
    >
      <van-tabbar-item to="/cookbook">
        <span>菜谱大全</span>
        <template #icon="props">
          <img :src="props.active ? cookbookActive : cookbook" alt="" />
        </template>
      </van-tabbar-item>
      <van-tabbar-item to="/category">
        <span>分类</span>
        <template #icon="props">
          <img :src="props.active ? menuActive : menu" alt="" />
        </template>
      </van-tabbar-item>
      <van-tabbar-item to="/more">
        <span>更多</span>
        <template #icon="props">
          <img :src="props.active ? moreActive : more" alt="" />
        </template>
      </van-tabbar-item>
    </van-tabbar>
  </div>
</template>

<style lang="scss">
.index-container {
  height: 100%;
  display: flex;
  flex-direction: column;
}
/* .van-tabbar--fixed {
  bottom: 34px;
} */
.van-nav-bar__title {
  color: #fff;
}
.van-nav-bar__content {
  background-color: palevioletred;
}

main {
  flex: 1;
  overflow-y: scroll;
}
</style>


