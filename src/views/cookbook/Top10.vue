<script setup>
import useListStore from "@/store/listStore";
const listStore = useListStore();
</script>

<template>
  <ul>
    <li v-for="li in listStore.filteredList(10)" :key="li.id">
      <img :src="li.img" alt="" />
      <div>
        <h1>{{ li.name }}</h1>
        <h2>{{ li.favorites }}收藏 {{ li.all_click }}浏览</h2>
      </div>
    </li>
  </ul>
</template>

<style lang="scss" scoped>
ul {
  display: flex;
  flex-wrap: wrap;
  background-color: #f5f5f5;
  padding-left: 10px;
  padding-top: 15px;
  li {
    width: 50%;
    padding-right: 10px;
    padding-bottom: 10px;
    img {
      width: 100%;
      display: block;
    }
    > div {
      background-color: #fff;
      padding: 5px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      h1,
      h2 {
        padding: 0;
        margin: 0;
        font-style: normal;
        font-weight: 400;
      }
      h1 {
        font-size: 22px;
      }
      h2 {
        font-size: 12px;
      }
    }
  }
}
</style>
