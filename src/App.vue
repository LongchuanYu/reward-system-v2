<script setup>
import {ref} from 'vue'
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
const active = ref(0)
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
