<template>
  <!-- 协议以及声明 -->
  <view class="list">
    <view class="lsit-item"
          @click="goAgreementRight">
      <view>权利声明</view>
      <image src="../../static/images/right-arrow.png"></image>
    </view>
    <view class="lsit-item"
          @click="goAgreementService">
      <view>服务协议</view>
      <image src="../../static/images/right-arrow.png"></image>
    </view>
    <view class="lsit-item"
          @click="goAgreementPrivacy">
      <view>隐私政策</view>
      <image src="../../static/images/right-arrow.png"></image>
    </view>
    <view class="lsit-item"
          @click="goAgreementKnowledge">
      <view>知识产权声明</view>
      <image src="../../static/images/right-arrow.png"></image>
    </view>
  </view>
</template>

<script>
export default {
  data () {
    return {

    }
  },
  methods: {
    // 去权利声明页面
    goAgreementRight () {
      uni.navigateTo({
        url: '/pages/agreementRight/agreementRight'
      });
    },
    // 去服务协议页面
    goAgreementService () {
      uni.navigateTo({
        url: '/pages/agreementService/agreementService'
      });
    },
    // 去隐私政策页面
    goAgreementPrivacy () {
      uni.navigateTo({
        url: '/pages/agreementPrivacy/agreementPrivacy'
      });
    },
    // 去知识产权声明
    goAgreementKnowledge () {
      uni.navigateTo({
        url: '/pages/agreementKnowledge/agreementKnowledge'
      });
    }
  }
}
</script>

<style>
.list {
  margin-top: 20rpx;
}
.lsit-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
  padding: 0 20rpx;
  margin-bottom: 6rpx;
}
.lsit-item view {
  width: 100%;
  height: 100rpx;
  line-height: 100rpx;
  font-size: 30rpx;
  color: #000;
}
.lsit-item image {
  width: 30rpx;
  height: 30rpx;
}
</style>
