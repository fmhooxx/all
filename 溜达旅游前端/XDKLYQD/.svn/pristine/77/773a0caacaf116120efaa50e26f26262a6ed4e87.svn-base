<template>
  <!-- 退款页面 -->
  <view class="confirmation-order">
    <view class="order-head">
      <!-- 头部区域 -->
      <view class="head">{{orderDetails.ProductName}}</view>
      <view class="order-common order-num">
        退款原因:
        <text class="reason">{{orderDetails.RefundReason}}</text>
      </view>
      <view class="order-common">
        申请时间:
        <text>{{orderDetails.ApplyRefundTime}}</text>
      </view>
      <view class="order-common">
        退款金额:
        <text>¥{{refundAmount}}</text>
      </view>
    </view>
    <!-- 预定人信息 -->
    <view class="order-head">
      <view class="order-title">预订人信息</view>
      <view class="order-content">
        <text>预订人</text>
        <text class="common-text">{{orderDetails.Contact}}</text>
      </view>
      <view class="order-content">
        <text>手机号</text>
        <text class="common-text">{{orderDetails.ContactPhone}}</text>
      </view>
    </view>
    <!-- 游客信息 -->
    <view class="order-head">
      <view class="order-title">游客信息</view>
      <view v-for="(item, index) in tourist"
            :key="index">
        <view class="order-content">
          <text>姓名</text>
          <text class="common-text">{{item.UserName}}</text>
        </view>
        <view class="order-content">
          <text>身份证</text>
          <text class="common-text">{{item.IDCard}}</text>
        </view>
      </view>
    </view>
    <!-- 退款进程 -->
    <view class="refund-footer">
      <view>退款进程</view>
      <view class="refun-footer-state">退款中</view>
    </view>
    <view class="shelter"></view>
    <view class="next"
          @click="goContact">
      <!-- <view class="next-one">
        <image src="/static/images/zixun.png"></image>
      </view> -->
      <view style="line-height: 50rpx;">联系客服</view>
    </view>
  </view>
</template>

<script>
import { GetProductOrderUserList, getOrderReservationsDetails } from '../api/agreement'
export default {
  data () {
    return {
      // 订单 id
      OrderID: '',
      // 订单详情
      orderDetails: '',
      // 游客信息
      tourist: '',
      // 退款金额
      refundAmount: ''
    };
  },
  methods: {
    // 获取当前游客的数据
    getOrder () {
      var result = {
        action: 'GetProductOrderUserList',
        userID: uni.getStorageSync('UserId'),
        OrderID: this.OrderID
      }
      GetProductOrderUserList(result).then(res => {
        console.log(res)
        if (res.data.status == true) {
          this.tourist = res.data.Data
        }
      })
    },
    // 获取订单预订人详情内容
    getOrderDetails () {
      var result = {
        action: 'GetProductOrderListByPage',
        userID: uni.getStorageSync('UserId'),
        OrderID: this.OrderID
      }
      getOrderReservationsDetails(result).then(res => {
        console.log(res)
        if (res.data.status == true) {
          this.orderDetails = res.data.Data.Data[0]
        }
      })
    },
    // 去客服页面
    goContact () {
      uni.switchTab({
        url: '/pages/contact/contact'
      });
    }
  },
  onLoad (options) {
    this.OrderID = options.OrderID
    this.refundAmount = options.refundAmount
    if (this.OrderID != undefined) {
      // 获取当前游客的数据
      this.getOrder(),
        // 获取订单预订人详情内容
        this.getOrderDetails()
    }
  }
};
</script>

<style>
/* 头部区域 */
.order-head {
  background-color: #fff;
  box-sizing: border-box;
  padding: 30rpx 30rpx 30rpx 50rpx;
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
.reason {
  text-overflow: -o-ellipsis-lastline;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  line-clamp: 2;
  -webkit-box-orient: vertical;
}
.order-common {
  margin: 10rpx 0;
  font-size: 28rpx;
  color: #818181;
}

.order-common text {
  margin-left: 30rpx;
}

.order-num {
  margin-bottom: 20rpx;
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
.refund-footer {
  padding: 15rpx 50rpx 15rpx 50rpx;
  background-color: #fff;
  display: flex;
  justify-content: space-between;
}
.refund-footer view {
  font-size: 32rpx;
  color: #525252;
  font-weight: 500;
}
.refund-footer .refun-footer-state {
  font-size: 28rpx;
  color: #d03434;
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
  font-size: 20rpx;
  background-color: #f0c462;
  color: #fff;
  z-index: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.next image {
  width: 100%;
  height: 100%;
}
.next-one {
  width: 46rpx;
  height: 46rpx;
}
</style>