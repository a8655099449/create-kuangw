<!--
 * @Author: liuxiang liuxiang@163.com
 * @Date: 2023-02-27 11:07:02
 * @LastEditors: liuxiang liuxiang@163.com
 * @LastEditTime: 2023-03-10 16:08:41
 * @FilePath: /vue-ts-threejs/src/pages/index.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
  <view class="content-bg">
    <view class="text-p" @click="goNext"> 首页 </view>
    <view class="content-p" @click="goSave()">点击使用vuex保存</view>
    {{ userInfo }}
  </view>
</template>

<script setup>
import { computed } from 'vue';
import { useStore } from 'vuex';

const store = useStore();
const env = import.meta.env;
console.log('获取的当前环境变量', env);
const userInfo = computed(() => store.state.index.userInfo);
const goNext = () => {
  uni.navigateTo({
    url: '/mine',
  });
};

const goSave = () => {
  uni.showLoading({
    title: '保存中...',
  });
  store.dispatch('updataUserInfo').then((data) => {
    console.log('用户数据保存成功', data);
    uni.hideLoading();
    uni.showToast({
      icon: 'none',
      title: '用户数据保存成功',
    });
  });
};
</script>

<style lang="scss" scoped>
.content-bg {
  .text-p {
    font-size: 50rpx;
    font-weight: 500;
    text-align: center;
    width: 100%;
    height: 200rpx;
    line-height: 200rpx;
    margin-top: 200rpx;
    color: red;
  }

  .content-p {
    font-size: 30rpx;
    text-align: center;
    width: 100%;
    height: 30rpx;
    line-height: 30rpx;
    margin-top: 30rpx;
    color: red;
  }
}
</style>
