<script setup>
import { ref } from "vue";
import { useRoute, useRouter } from "vue-router";
const route = useRoute();
const router = useRouter();
const name = ref("")
const money = ref("")
const image = ref("")

function goback() {
  router.back();
}

function onSubmit() {
  plus.io

}
</script>

<template>
  <div>
    <van-nav-bar
      title="编辑"
      left-text="返回"
      left-arrow
      @click-left="goback"
      style="margin-bottom: 10px;"
    />
    <van-form @submit="onSubmit">
      <van-cell-group inset>
        <van-field
          v-model="name"
          name="name"
          label="事件名"
        />
        <van-field
          v-model="money"
          name="money"
          label="价格"
        />
        <van-field
          v-model="image"
          name="image"
          label="图片"
        />
      </van-cell-group>
      <div style="margin: 16px">
        <van-button round block type="primary" native-type="submit">
          提交
        </van-button>
      </div>
    </van-form>
  </div>
</template>

<style scoped></style>
