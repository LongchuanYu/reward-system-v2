<script setup>
import {ref} from 'vue'
const records = ref([
  {
    name: '倒垃圾戳粑粑',
    money: 10,
    img: "https://img.zcool.cn/community/0140415976d8c4a8012193a34591b4.jpg@1280w_1l_2o_100sh.jpg"
  },
  {
    name: '倒垃圾戳粑粑',
    money: 10,
    img: "https://img.zcool.cn/community/0140415976d8c4a8012193a34591b4.jpg@1280w_1l_2o_100sh.jpg"
  }
])

function gotoEdit() {
  console.log('gotoEdit')
}
</script>

<template>
  <div>
    <van-list>
      <van-row v-for="(item, index) in records" :key="index" @click="gotoEdit(item)">
        <van-col span="2" justify="center">
          <van-image height="23px" :src="item.img"></van-image>
        </van-col>
        <van-col span="10"> {{ item.name }} </van-col>
        <van-col span="10">{{ item.money }}元</van-col>
        <van-col span="2"> > </van-col>
      </van-row>
    </van-list>
  </div>
</template>

<style scoped></style>
