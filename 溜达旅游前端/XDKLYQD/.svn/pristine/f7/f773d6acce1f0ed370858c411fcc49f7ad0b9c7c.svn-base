<template>
  <!-- 我的行程页面 -->
  <view>
    <view class="list"
          v-for="(item, index) in tabsList"
          :key="index">
      <view class="list-left">
        <view class="left-title">{{ item.ProductName }}</view>
        <view class="left-content">
          <image :src="item.ThumbnailUrl60"></image>
          <view class="content-text">
            <!-- <view>10人团</view> -->
            <view>{{ item.OpenDate }} 出发</view>
            <view class="price">¥{{ item.Amount }}</view>
          </view>
        </view>
      </view>
      <!-- <view class="list-right"
            @click="goCalendar">
        <view>查看</view>
        <image src="/static/images/right-arrow.png"></image>
      </view> -->
    </view>
    <view class="footer"
          v-if="isFlag">
      <image src="/static/images/chaxun.png"></image>
      <view>没有查询到相关足迹</view>
    </view>
  </view>
</template>

<script>
import { GetProductOrderListByPage } from '../api/agreement'
export default {
  data () {
    return {
      tabsList: [],
    }
  },
  methods: {
    // 获取订单数据
    getOrderList () {
      var result = {
        action: 'GetProductOrderListByPage',
        OrderStatus: 1,
        userID: uni.getStorageSync('UserId'),
      }
      GetProductOrderListByPage(result).then((res) => {
        if (res.data.status == true) {
          res.data.Data.Data.forEach((item, index) => {
            item.OpenDate = item.OpenDate.split(' ')[0]
          })
          this.tabsList = res.data.Data.Data
        }
      })
    },
    // 去图文详情页面
    goCalendar () {
      uni.navigateTo({
        url: '/pages/calendar/calendar',
      })
    },
  },
  onLoad () {
    // 获取订单数据
    this.getOrderList()
  },
  computed: {
    isFlag () {
      if (this.tabsList.length == 0) {
        return true
      }
      return false
    },
  },
}
</script>

<style>
.list {
  background-color: #fff;
  padding: 26rpx 20rpx;
  margin: 8rpx 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
}

.list-left {
  width: 84%;
}

.left-title {
  font-size: 30rpx;
  font-weight: 500;
  color: #545454;
  white-space: nowrap;
  /*一行显示*/
  overflow: hidden;
  /*超出部分隐藏*/
  text-overflow: ellipsis;
  /*用...代替超出部分*/
}

.left-content {
  display: flex;
  margin-top: 20rpx;
}

.left-content image {
  width: 135rpx;
  height: 135rpx;
  border-radius: 10rpx;
  margin-right: 30rpx;
}
.content-text {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.content-text view {
  font-size: 28rpx;
  color: #545454;
  font-weight: 400;
}

.content-text :nth-child(2) {
  margin: 10rpx 0;
}

.content-text .price {
  font-size: 28rpx;
  color: #d03434;
  font-weight: 400;
}

.list-right {
  display: flex;
  justify-content: center;
  align-items: center;
}

.list-right view {
  font-size: 28rpx;
  color: #545454;
  margin-right: 10rpx;
}

.list-right image {
  width: 25rpx;
  height: 25rpx;
}

/* 无内容区域 */
.footer {
  margin-top: 200rpx;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.footer image {
  width: 84rpx;
  height: 84rpx;
}

.footer view {
  margin-top: 40rpx;
  font-size: 28rpx;
  color: #545454;
}
</style>
