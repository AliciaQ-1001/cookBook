<script setup>
import { ref } from "vue";
import useListStore from "@/store/listStore";
const listStore = useListStore();
const list = ref(listStore.filteredList(10));

const loading = ref(false);
const finished = ref(false);
const refreshing = ref(false);

const currentPage = ref(1);
const pageSize = ref(Math.ceil(listStore.list.length / 10));

const onLoad = () => {
  currentPage.value++;

  // data = await ajax()

  if (refreshing.value) {
    list.value = [];
    currentPage.value = 1;
    refreshing.value = false;
  }

  list.value = listStore.filteredList(currentPage.value * 10);

  loading.value = false;

  if (currentPage.value >= pageSize.value) {
    finished.value = true;
  }
};

const onRefresh = () => {
  // 清空列表数据
  finished.value = false;

  // 重新加载数据
  // 将 loading 设置为 true，表示处于加载状态
  loading.value = true;
  onLoad();
};
</script>

<template>
  <div>
    <van-pull-refresh v-model="refreshing" @refresh="onRefresh">
      <van-list
        v-model:loading="loading"
        :finished="finished"
        finished-text="没有更多了"
        @load="onLoad"
      >
        <ul>
          <li v-for="li in list" :key="li.id">
            <div>
              <img :src="li.img" alt="" />
            </div>
            <div>
              <h1>{{ li.name }}</h1>
              <h2>{{ li.burdens }}</h2>
              <h3>{{ li.favorites }}浏览 {{ li.all_click }}收藏</h3>
            </div>
          </li>
        </ul>
      </van-list>
    </van-pull-refresh>
  </div>
</template>

<style lang="scss" scoped>
@import "@/assets/border.scss";
div {
  ul {
    li {
      display: flex;
      padding-right: 10px;
      &:not(:last-child) {
        @include border(0 0 1px 0);
      }
      > div:first-child {
        padding: 10px 15px 10px 10px;
        img {
          width: 110px;
          height: 70px;
        }
      }
      > div:last-child {
        display: flex;
        flex-direction: column;
        justify-content: center;
        h1,
        h2,
        h3 {
          margin: 0;
          padding: 0;
          font-weight: normal;
        }
        h1 {
          font-size: 20px;
        }
        h2 {
          font-size: 16px;
          color: #aaa;

          display: -webkit-box;
          -webkit-box-orient: vertical;
          -webkit-line-clamp: 1;
          overflow: hidden;
        }
        h3 {
          font-size: 14px;
          color: #aaa;
        }
      }
    }
  }
}
</style>
