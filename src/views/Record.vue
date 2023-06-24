<script setup>
import { ref, computed } from "vue";
const value1 = ref(0);
const option1 = ref([
  {
    text: 'ly',
    value: 0
  },
  {
    text: 'dxx',
    value: 1
  }
])
const records = ref([
  {
    time: '2023-01-01 14:00:00',
    who: 'dxx',
    what: '倒垃圾',
    money: 15
  }
])
</script>

<template>
  <div>
    <van-dropdown-menu class="drop-down">
      <van-dropdown-item v-model="value1" :options="option1" />
    </van-dropdown-menu>

    <van-list>
      <van-row>
        <van-col span="10" justify="center">
          <span>2023-01-01 14:00:00</span>
        </van-col>
        <van-col span="4"> dxx </van-col>
        <van-col span="8"> 倒垃圾 </van-col>
        <van-col span="2"> 15 </van-col>
      </van-row>
    </van-list>
  </div>
</template>

<style scoped>
.drop-down {
  margin-bottom: 20px;
}
</style>
