<template>
  <!-- 客服页面 -->
  <view>
    <view style="margin-top: 20rpx;">
      <button class="btn common"
              open-type="contact"
              @contact="handle">微信客服</button>
      <view class="common tel"
            @click="goMakePhoneCall">电话客服</view>
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
    handle (e) {
      console.log(e)
    },
    // 拨打号码
    goMakePhoneCall () {
      uni.makePhoneCall({
        phoneNumber: '0575-87597627' //仅为示例
      });
    }
  }
}
</script>

<style>
.btn {
  border-radius: 0;
}

.btn::after {
  border: none;
  border-radius: 0;
}

.common {
  font-size: 32rpx;
  color: #737c84;
  width: 700rpx;
  height: 98rpx;
  background-color: #fff;
  box-shadow: 0rpx 9rpx 16rpx 0rpx rgba(234, 234, 234, 0.5);
}

.tel {
  line-height: 98rpx;
  text-align: center;
  margin: 20rpx auto;
}
</style>