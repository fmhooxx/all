<template>
  <!-- 确认订单页面 -->
  <view class="confirmation-order">
    <view class="order-head">
      <!-- 头部区域 -->
      <view class="head">宁波象山: 一日豪华游 东方不老岛、海山仙子岛，享受自然原原生态</view>
      <!-- <view class="order-common order-num">
        订单编号:
        <text>202003260001</text>
      </view>
      <view class="order-common">
        下单时间:
        <text>{{time}}</text>
      </view> -->
    </view>
    <!-- 出发日期 -->
    <view class="order-common go-data">
      出发日期:
      <text>2020-03-28</text>
    </view>
    <!-- 预定人信息 -->
    <view class="order-head">
      <view class="order-title">预订人信息</view>
      <view class="order-content">
        <text>预订人</text>
        <text class="common-text">雄登康</text>
      </view>
      <view class="order-content">
        <text>手机号</text>
        <text class="common-text">17812345689</text>
      </view>
    </view>
    <!-- 游客信息 -->
    <view class="order-head">
      <view class="order-title">游客信息</view>
      <view class="order-content">
        <text>姓名</text>
        <text class="common-text">雄登康(成人)</text>
      </view>
      <view class="order-content">
        <text>身份证</text>
        <text class="common-text">342425178564852115</text>
      </view>
    </view>
    <!-- 费用明细 -->
    <view class="order-head">
      <view class="order-title">费用明细</view>
      <view class="order-content">
        <text>成人</text>
        <text class="common-text">
          ¥299
          <text>*</text>1
        </text>
      </view>
      <view class="order-content">
        <text>儿童</text>
        <text class="common-text">
          ¥199
          <text>*</text>1
        </text>
      </view>
      <view class="order-content order-footer">
        <text>合计</text>
        <text class="common-text">¥498</text>
      </view>
    </view>
    <view class="shelter"></view>
    <view class="next"
          @click="goPaymentOrder">下一步</view>
  </view>
</template>

<script>
export default {
  data () {
    return {
      // 当前的时间、日期
      time: null,
      // 支付凭证
      voucherNumber: "",
      // 订单 id
      orderId: ''
    };
  },
  methods: {
    // 去支付订单页面
    goPaymentOrder () {
      uni.navigateTo({
        url: "/pages/paymentOrder/paymentOrder"
      });
    },
    // 获取当前的日期
    getTime () {
      var date = new Date(),
        year = date.getFullYear(),
        month = date.getMonth() + 1,
        day = date.getDate(),
        hour = date.getHours() < 10 ? "0" + date.getHours() : date.getHours(),
        minute =
          date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes(),
        second =
          date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds();
      month >= 1 && month <= 9 ? (month = "0" + month) : "";
      day >= 0 && day <= 9 ? (day = "0" + day) : "";
      var timer =
        year +
        "-" +
        month +
        "-" +
        day +
        " " +
        hour +
        ":" +
        minute +
        ":" +
        second;
      this.time = timer;

      return timer;
    }
  },
  onLoad (options) {
    this.voucherNumber = options.voucherNumber;
    this.orderId = options.orderId
    console.log(this.orderId)
    this.getTime();
  }
};
</script>

<style>
/* 头部区域 */
.order-head {
  background-color: #fff;
  box-sizing: border-box;
  padding: 30rpx;
  margin-bottom: 10rpx;
}

.head {
  font-size: 36rpx;
  font-weight: 500;
  color: #525252;
  margin-bottom: 20rpx;
  text-overflow: -o-ellipsis-lastline;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  line-clamp: 2;
  -webkit-box-orient: vertical;
}

.order-common {
  font-size: 28rpx;
  color: #818181;
}

.order-common text {
  margin-left: 30rpx;
}

.order-num {
  margin-bottom: 20rpx;
}

.go-data {
  height: 60rpx;
  line-height: 60rpx;
  padding-left: 30rpx;
  background-color: #fff;
  margin: 20rpx 0;
}

/* 相同的 title */
.order-title {
  font-size: 32rpx;
  color: #525252;
  font-weight: 500;
  margin-bottom: 20rpx;
}

/* 相同的 content */
.order-content {
  font-size: 28rpx;
  color: #525252;
  margin: 20rpx 0;
  display: flex;
  justify-content: space-between;
}

/* 相同的 text */
.common-text {
  width: 82%;
}

.order-footer {
  color: red;
}

.shelter {
  width: 100%;
  height: 98rpx;
}

.next {
  position: fixed;
  bottom: 0;
  height: 98rpx;
  line-height: 98rpx;
  text-align: center;
  width: 100%;
  font-size: 36rpx;
  background-color: #f0c462;
  color: #fff;
  z-index: 1;
}
</style>