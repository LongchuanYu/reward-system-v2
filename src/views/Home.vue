<script setup>
import { ref, computed } from "vue";
import { showConfirmDialog } from 'vant';
import 'vant/es/dialog/style';
const awardItem = ref([{
  name: "倒垃圾",
  img: "https://img.zcool.cn/community/0140415976d8c4a8012193a34591b4.jpg@1280w_1l_2o_100sh.jpg",
  money: 5
},{
  name: "倒垃圾",
  img: "https://img.zcool.cn/community/0140415976d8c4a8012193a34591b4.jpg@1280w_1l_2o_100sh.jpg",
  money: 150
},{
  name: "倒垃圾",
  img: "https://img.zcool.cn/community/0140415976d8c4a8012193a34591b4.jpg@1280w_1l_2o_100sh.jpg",
  money: 5
},{
  name: "倒垃圾",
  img: "https://img.zcool.cn/community/0140415976d8c4a8012193a34591b4.jpg@1280w_1l_2o_100sh.jpg",
  money: 5
}]);
const touchPos = ref([0, 0])
const isDrag = ref(false)
const dxxRef = ref()
const dxxMoney = ref(0)
const dxxCurMoney = ref(0)
const lyRef = ref()
const lyMoney = ref(0)
const lyCurMoney = ref(0)
let timeoutEvent;
const virtualPos = computed(() => {
  return {
    left: touchPos.value[0] - 10 - 50,
    top: touchPos.value[1] - 10 - 50,
  }
})
const virtualStyle = computed(() => {
  return {
    left: virtualPos.value.left + 'px',
    top: virtualPos.value.top + 'px'
  }
})

function touchstart(e) {
    console.log(dxxRef.value.getBoundingClientRect())
    console.log(lyRef.value.getBoundingClientRect())
  timeoutEvent = setTimeout(() => {
    e.preventDefault();
    console.log(e);
    timeoutEvent = 0;
    isDrag.value = true;
    updatetouchPos(e);
  }, 500);
}

function touchmove(e) {
  clearTimeout(timeoutEvent)
  if (timeoutEvent === 0) {
    e.preventDefault();
    updatetouchPos(e);
  }
}

function touchcancel(e) {
  clearTimeout(timeoutEvent)
  isDrag.value = false
}

function touchend(e, item) {
  console.log(item)
  clearTimeout(timeoutEvent)
  if (timeoutEvent === 0) {
    isDrag.value = false
    const dxxRect = dxxRef.value.getBoundingClientRect()
    const lyRect = lyRef.value.getBoundingClientRect()
    if (virtualPos.value.left > dxxRect.left && virtualPos.value.left < dxxRect.right && virtualPos.value.top > dxxRect.top && virtualPos.value.top < dxxRect.bottom) {
      addMoney('dxx')
    } else if (virtualPos.value.left > lyRect.left && virtualPos.value.left < lyRect.right && virtualPos.value.top > lyRect.top && virtualPos.value.top < lyRect.bottom) {
      addMoney('ly')
    }
  }
}

function addMoney(who) {
  console.log(who)
  showConfirmDialog({
    title: '提示',
    message: `确定要给${who}加钱吗？`,
  }).then(() => {
    if (who === 'dxx') {
      // todo
      dxxMoney.value += 1
    } else {
      lyMoney.value += 1
    }
  }).catch(() => {});
}

function updatetouchPos(e) {
  const clientX = e.changedTouches[0].clientX
  const clientY = e.changedTouches[0].clientY
  touchPos.value[0] = clientX
  touchPos.value[1] = clientY
}
</script>

<template>
<div class="container">
  <div class="header">
    <div class="header-item" ref="dxxRef">
      <img src="../assets/ft.png" alt="" />
      <span class="money">总计：{{dxxMoney}}元</span>
      <span class="money-cur">当前：{{dxxCurMoney}}元</span>
    </div>
    <div class="header-item" ref="lyRef">
      <img src="../assets/fg.png" alt="" />
      <span class="money">总计：{{lyMoney}}元</span>
      <span class="money-cur">当前：{{lyCurMoney}}元</span>
    </div>
  </div>
  <div class="fn-tools">
    <van-button type="primary" size="small" plain>结清当前</van-button>
  </div>
  <hr />
  <div class="award">
    <van-grid column-num="2" gutter="10" icon-size="50px">
      <van-grid-item
        :icon="item.img"
        v-for="(item, index) in awardItem"
        :key="index"
        :badge="item.money + '元'"
        @touchstart="touchstart($event)"
        @touchmove="touchmove($event)"
        @touchcancel="touchcancel($event)"
        @touchend="touchend($event, item)"
      >
        <template #text>
          <span @contextmenu="e=>e.preventDefault()" @selectstart="e=>e.preventDefault()">
            {{item.name}}
          </span>
        </template>
      </van-grid-item>
    </van-grid>
  </div>
  <div class="virtual-item" v-if="isDrag" :style="virtualStyle">red</div>
</div>
</template>

<style scoped>
.container {
  position: relative;
}
.virtual-item {
  position: absolute;
}
.header {
  display: flex;
  justify-content: center;
  height: 30vh;
  margin-bottom: 20px;
}
.header img {
  width: 100%;
}
.header-item {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.money {
  color: #f00;
}
.fn-tools {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.award {
  margin-top: 20px;
  overflow: auto;
  height: calc(100vh - 30vh - 100px)
}
</style>
