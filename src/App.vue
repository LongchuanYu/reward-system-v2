<script setup>
import {ref, watch} from 'vue'
import { RouterLink, RouterView, useRoute } from "vue-router";
const active = ref()
const route = useRoute()
watch(route, () => {
  console.log(route.name);
  switch (route.name) {
    case 'home':
      active.value = 0
      break;
    case 'record':
      active.value = 1
      break;
    case 'manager':
      active.value = 2
      break;
  }
})
</script>

<template>
  <RouterView />
  <van-tabbar v-model="active">
    <van-tabbar-item icon="home-o" to="/">主页</van-tabbar-item>
    <van-tabbar-item icon="search" to="/record">记录</van-tabbar-item>
    <van-tabbar-item icon="friends-o" to="/manager">管理</van-tabbar-item>
  </van-tabbar>
</template>

<style scoped>
</style>
