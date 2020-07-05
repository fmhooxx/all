<template>
  <!-- 订单列表页面 -->
  <view>
    <view>
      <!-- tab 栏区域 -->
      <view class="tab-box">
        <view class="tab">
          <view v-for="item in tabs"
                :key="item.id"
                :class="active == item.id ? 'selection' : ''"
                @click="tabsChange(item.id)">{{ item.text }}
          </view>
        </view>
      </view>
      <!-- tab 栏下面的内容 -->
      <view class="list">
        <!-- 已完成的状态 -->
        <view v-if="active == 2">
          <view class="list-item"
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
            <view class="list-right">
              <view @click="goOrderDetails(item.OrderID)">查看</view>
              <image src="/static/images/right-arrow.png"></image>
            </view>
          </view>
        </view>
        <!-- 待出行状态 -->
        <view v-if="active == 1">
          <view class="list-item"
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
            <view class="list-right">
              <view @click="refund(item.OrderID, item.RefundRulesGroupID)">退款</view>
              <image src="/static/images/right-arrow.png"></image>
            </view>
          </view>
        </view>
        <!-- 待支付状态 -->
        <view v-if="active == 0">
          <view class="list-item"
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
            <view class="list-right">
              <view style="color: #4eb4a0;"
                    @click="goPaymentOrder(item.PayVoucherNumber,item.Amount)">支付</view>
              <image src="/static/images/right-arrow.png"></image>
            </view>
          </view>
        </view>
        <!-- 已过期状态 -->
        <view v-if="active == 4">
          <view class="list-item"
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
            <view class="list-right">
              <view>已关闭</view>
            </view>
          </view>
        </view>
        <!-- 退款单状态 -->
        <view v-if="active == 3">
          <view class="list-item"
                v-for="(item, index) in tabsList"
                :key="index">
            <view class="list-left">
              <view class="left-title">{{ item.ProductName }}</view>
              <view class="left-content">
                <image :src="item.ThumbnailUrl60"></image>
                <view class="content-text">
                  <!-- <view>10人团</view> -->
                  <view>{{ item.OpenDate }} 出发</view>
                  <view class="price">¥{{ item.RefundAmount }}</view>
                </view>
              </view>
            </view>
            <view class="list-right">
              <view class="refund"
                    v-if="item.RefundStatus == 0">未退款</view>
              <view class="refund"
                    v-if="item.RefundStatus == 1">退款中</view>
              <view class="refund"
                    v-if="item.RefundStatus == 3">退款成功</view>
              <view class="refund"
                    v-if="item.RefundStatus == 4">拒绝退款</view>
            </view>
          </view>
        </view>
        <view class="footer"
              v-if="isFlag">
          <image src="/static/images/chaxun.png"></image>
          <view>没有查询到相关足迹</view>
        </view>
      </view>
    </view>
    <!-- <view class="footer"
          v-else>
      <image src="/static/images/chaxun.png"></image>
      <view>没有查询到相关足迹</view>
    </view> -->
  </view>
</template>

<script>
export default {
  data () {
    return {
      // tab 栏数据
      tabs: [
        {
          text: '已完成',
          id: 2,
        },
        {
          text: '待出行',
          id: 1,
        },
        {
          text: '待支付',
          id: 0,
        },
        {
          text: '已过期',
          id: 4,
        },
        {
          text: '退款单',
          id: 3,
        },
      ],
      // 默认选中项
      active: 2,
      // 控制有内容和没有内容页面之间的切换显示
      // tab 栏下面的数据
      flag: true,
      tabsList: [],
      page: {
        // 当前页
        pageIndex: 1,
        // 当前页面显示的条数
        pageSize: 6,
      },
      // 总的数据条数
      total: ''
    }
  },
  methods: {
    // 点击 tab 栏时 触发
    tabsChange (id) {
      this.active = id
      this.page.pageSize = 6
      this.page.pageIndex = 1
      this.tabsList = []
      this.GetProductOrderListByPage()
    },
    // 去订单详情页面
    goOrderDetails (OrderID) {
      console.log(OrderID)
      uni.navigateTo({
        url: '/pages/orderDetails/orderDetails?OrderID=' + OrderID,
      })
    },
    // 去支付页面
    goPaymentOrder (PayVoucherNumber, Amount) {
      uni.navigateTo({
        url:
          '/pages/paymentOrder/paymentOrder?PayVoucherNumber=' +
          PayVoucherNumber + '&Amount=' + Amount
      })
    },
    // 去我的行程
    goTrip () {
      uni.navigateTo({
        url: '/pages/trip/trip',
      })
    },
    // 去退款页面
    refund (OrderID, RefundRulesGroupID) {
      uni.navigateTo({
        url: '/pages/refund/refund?OrderID=' + OrderID + '&RefundRulesGroupID=' + RefundRulesGroupID,
      })
    },
    // 获取订单数据
    GetProductOrderListByPage () {
      this.$http
        .post('/api/WeiXinApplet.ashx', {
          action: 'GetProductOrderListByPage',
          OrderStatus: this.active,
          userID: uni.getStorageSync('UserId'),
          pageIndex: this.page.pageIndex,
          pageSize: this.page.pageSize,
        })
        .then((res) => {
          this.total = res.data.Data.TotalRecords
          if (res.data.status == true) {
            res.data.Data.Data.forEach((item, index) => {
              item.OpenDate = item.OpenDate.split(' ')[0]
            })
            this.tabsList.push(...res.data.Data.Data)
            var result = this.tabsList.length
            this.flag = true
          }
          if (this.total == result) {
            this.flag = false
          }
        })
    },
    // 上拉加载更多
    onReachBottom (e) {
      this.page.pageIndex += 1
      // this.page.pageSize += 4
      if (this.flag) {
        this.GetProductOrderListByPage()
      } else {
        uni.showToast({
          title: '我是有底线的',
          duration: 2000,
          icon: 'none',
          duration: 2000,
        })
      }
    },
  },
  computed: {
    isFlag () {
      if (this.tabsList.length == 0) {
        return true
      }
      return false
    },
  },
  onLoad (options) {
    if (options.active != undefined) {
      this.active = options.active
    }
    // 获取订单数据
    this.GetProductOrderListByPage()
  },
}
</script>

<style>
/* tab 栏区域 */
/* 选中的文字颜色 */
.selection {
  color: #4eb4a0 !important;
  border-bottom: 4rpx solid #4eb4a0 !important;
  transition: all 0.3s;
}
.tab-box {
  position: fixed;
  top: 0;
  width: 100%;
}
.tab {
  height: 90rpx;
  background-color: #fff;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}

.tab view {
  height: 100%;
  font-size: 28rpx;
  color: #545454;
  line-height: 90rpx;
  border-bottom: 4rpx solid transparent;
}

/* tab 栏下面的内容 */
.list {
  /* background-color: #fff; */
  /* padding: 26rpx 20rpx; */
  margin: 90rpx 0;
}
.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10rpx;
  background-color: #fff;
}
.list-left {
  width: 80%;
  padding: 26rpx 20rpx;
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
  margin-right: 10rpx;
}

.list-right view {
  font-size: 28rpx;
  color: #545454;
  margin-right: 10rpx;
}

.list-right image {
  width: 25rpx;
  height: 25rpx;
  margin-top: 5rpx;
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

.refund {
  width: 116rpx;
  height: 243rpx;
  line-height: 243rpx;
  text-align: center;
  background-color: #e8e8e8;
  font-size: 28rpx;
  color: #636363;
}
</style>
