<template>
  <!-- 图文详情页面 -->
  <view>
    <!-- 头部照片区域 -->
    <view class="banner">
      <image :src="details.ImageUrl1"
             mode="scaleToFill"></image>
      <view class="banner-content">
        <view class="banner-title">{{details.ProductName}}</view>
        <view class="banner-price">¥{{details.MaxShowPrice}}起/人</view>
      </view>
    </view>
    <!-- 订单相关信息 -->
    <view class="order-box">
      <view>产品编号:<text>{{details.chanpingbianhao}}</text></view>
      <view>出发到达:<text>{{details.chufadaoda}}</text></view>
      <view>出游天数:<text>{{details.chuyoutianshu}}；{{details.chuyoufangshi}}</text></view>
      <view>交通方式:<text>{{details.jiaotongfangshi}}</text></view>
      <view>住宿标准:<text>{{details.zhusubiaozhun}}</text></view>
      <view>经典景点:<text>{{details.jingdianjingdian}}</text></view>
    </view>
    <!-- 线路特色 -->
    <view class="characteristic">
      <view class="characteristic-title">线路特色</view>
      <rich-text :nodes="textVal"></rich-text>
    </view>
    <!-- 行程介绍 -->
    <view class="introduce">
      <view class="introduce-title">行程介绍</view>
      <view class="introduce-text">此行程为出发地参团</view>
      <view class="introduce-content"
            v-for="(item, index) in tripIntroduce"
            :key="index">
        <view class="place">{{item.Name}}</view>
        <view>集合时间: <text>{{item.jiheshijian}}</text></view>
        <view>集合地点: <text>{{item.jihedidian}}</text></view>
        <view>具体行程:</view>
        <view>{{item.jutixingcheng}}</view>
      </view>
      <!-- <view class="introduce-content">
				<view class="place">绍兴-宁波</view>
				<view>集合地点: <text>8:10</text></view>
				<view>集合地点: <text>诸暨市车站门口</text></view>
				<view>具体行程:</view>
				<view>【9:30】到达景点，由导游统一办理入园门票，入园后自由活动</view>
				<view>【11:00】享用团队餐：特色餐厅，享受海边鲜美海鲜大餐</view>
				<view>【12:00】自由活动，可前往海边拍照观赏【19:00】观赏夜景，享受自然夜景风光</view>
				<view>【20:00】集合返回绍兴，结束愉快旅程</view>
			</view> -->
    </view>
    <!-- 费用介绍 -->
    <view class="cost">
      <view class="cost-title">费用介绍</view>
      <view class="cost-contain">费用包含:</view>
      <view class="cost-content">
        <view>【用餐】{{details.yongcan}}</view>
        <view>【接送】{{details.jiesong}}</view>
        <view>【门票】{{details.menpiao}}</view>
        <view>【导游】{{details.daoyou}}</view>
      </view>
      <view class="cost-tips">
        <view class="cost-contain">温馨提示:</view>
        <view>{{details.wenxintishi}}</view>
      </view>
      <view class="cost-contain">费用不含:</view>
      <view class="cost-content">
        <view>【购物】{{details.gouwu}}</view>
        <view>【餐费】{{details.canfei}}</view>
      </view>
    </view>
    <!-- 购买须知区域 -->
    <view class="notice">
      <view class="notice-title">购买须知</view>
      <view class="cost-contain">退订政策</view>
      <view class="cost-content">
        <view v-for="(item, index) in refundRule"
              :key="index">{{index + 1}}、{{item.Contentss}}</view>
        <!-- <view>1.在行程开始前7天以外取消订单，退还费用100%；</view>
				<view>2.在行程开始前3天以外7天以内取消，退还费用50%；</view>
				<view>3.在行程开始前3天以内取消订单，费用不予退还。</view>
				<view>4.由于不可抗拒力因素产生退订，请联系客服，另行处理。</view> -->
      </view>
      <View class="cost-contain">温馨提示</View>
      <view class="cost-content">
        <view>
          【证件】{{details.zhengjian}}
        </view>
        <view>【其他】{{details.qita}}</view>
        <view>【衣物】{{details.yiwu}}</view>
      </view>
    </view>
    <view class="guarantee">
      <image src="/static/images/baohu.png"></image>
      <view>全程预定保障，溜达旅游陪您安全出游</view>
    </view>
    <!-- 固定定位区域 -->
    <view class="location-copy"></view>
    <view class="location">
      <view class="location-one"
            @click="goMakePhoneCall">
        <view style="height: 28rpx;">
          <image src="/static/images/zixun.png"></image>
        </view>
        <view>咨询</view>
      </view>
      <button v-if="isOpenid"
              class="location-two"
              open-type="getUserInfo"
              @getuserinfo="getLogin">立即购买没有</button>
      <button v-else
              class="location-two"
              @click="open">立即购买有</button>
    </view>
    <!-- 弹出框区域 -->
    <uniPopup ref="popup"
              type="center">
      <view class="box">
        <view class="box-title common">提示</view>
        <view class="box-content common">
          <view>系统检测到您未登录账号</view>
          <view>请先登录</view>
        </view>
        <view class="box-footer common"
              @click="goLogin">去登录</view>
      </view>
    </uniPopup>
    <!-- 分享区域 -->
    <view class="share-button">
      <button class="btn"
              open-type="share">
        <image class="img"
               src="/static/images/share.png"></image>
      </button>
    </view>
  </view>
</template>

<script>
import { GetRefundRules } from '../api/agreement'
import uniPopup from "@/components/uni-popup/uni-popup.vue"
export default {
  components: {
    uniPopup
  },
  data () {
    return {
      // openid
      openid: null,
      // 手机号码
      phoneNumber: null,
      // 线路特色富文本的内容
      textVal: '<h1>这是富文本内容</h1>',
      // 传递过来的 页面详情的 id
      ProductId: '',
      // 图文详情
      details: '',
      // 行程介绍
      tripIntroduce: '',
      // 退订规则
      refundRule: ''
    }
  },
  methods: {
    // 判断是否登录了 登录了下单 未去登录页面
    getLogin () {
      uni.login({
        provider: 'weixin',
        success: (res) => {
          var code = res.code
          this.$http.post('/api/WeiXinApplet.ashx', {
            action: "Login",
            code: code,
            ReferralUserId: uni.getStorageSync('ReferralUserId')
          }).then(res => {
            if (res.data.status == 'true') {
              uni.setStorageSync('openid', res.data.openid)
              uni.setStorageSync('session_key', res.data.session_key)
              uni.setStorageSync('UserId', res.data.UserId)
              if (res.data.UserId) {
                this.getUser()
              }
            } else {
              uni.showToast({
                title: '获取信息异常，请稍后重新操作！',
                duration: 2000,
                icon: 'none'
              });
            }
          })
        }
      });
    },
    // 获取用户信息
    getUser () {
      uni.getUserInfo({
        provider: 'weixin',
        success: (res) => {
          if (res.errMsg == 'getUserInfo:ok') {
            uni.setStorageSync('avatarUrl', res.userInfo.avatarUrl)
            uni.setStorageSync('nickName', res.userInfo.nickName)
            this.$http.post('/api/WeiXinApplet.ashx', {
              action: 'UserBindInfo',
              UserId: uni.getStorageSync('UserId'),
              nickName: res.userInfo.nickName,
              gender: res.userInfo.gender,
              avatarUrl: res.userInfo.avatarUrl
            }).then(res => {
              if (res.data.status == 'true') {
                uni.navigateTo({
                  url: '/pages/login/login?ProductId=' + this.ProductId
                });
              }
            })
          }
        }
      });
    },
    // 打开弹出框
    open () {
      // 如果手机号码为空 打开弹框
      if (this.phoneNumber == '') {
        this.$refs.popup.open()
      } else {
        // 去选择出行时间 / 人数页面
        uni.navigateTo({
          url: '/pages/choice/choice?productId=' + this.ProductId + '&MaxShowPrice=' + this.MaxShowPrice
        });
      }
    },
    // 去登录页面
    goLogin () {
      uni.navigateTo({
        url: '/pages/login/login?ProductId=' + this.ProductId
      });
    },
    // 获取详情内容
    GetProductByID () {
      this.$http.post('/api/WeiXinApplet.ashx', {
        action: 'GetProductByID',
        productId: this.ProductId
      }).then(res => {
        console.log(res)
        if (res.data.status == true) {
          this.details = res.data.Data
          this.MaxShowPrice = res.data.Data.MaxShowPrice
          // 线路特色
          this.textVal = res.data.Data.Description
          // 获取退款规则
          var refundRulesGroupID = res.data.Data.RefundRulesGroupID
          var result = {
            action: 'GetRefundRules',
            RefundRulesGroupID: refundRulesGroupID
          }
          GetRefundRules(result).then(res => {
            this.refundRule = res.data.Data
          })
        }
      })
    },
    // 获取行程介绍的内容
    GetProductTripByProductID () {
      this.$http.post('/api/WeiXinApplet.ashx', {
        action: 'GetProductTripByProductID',
        productId: this.ProductId
      }).then(res => {
        console.log(res)
        if (res.data.status == true) {
          this.tripIntroduce = res.data.Data.Data
        }
      })
    },
    // 拨打号码
    goMakePhoneCall () {
      uni.switchTab({
        url: '/pages/contact/contact'
      });
    }
  },
  // 分享
  onShareAppMessage (res) {
    var UserId = uni.getStorageSync('UserId')
    if (res.from === 'button') {// 来自页面内分享按钮
      return {
        title: this.details.ProductName,
        path: '/pages/contentDetails/contentDetails?UserId=' + UserId + '&ProductId=' + this.ProductId
      }
    } else {
      return {
        title: this.details.ProductName,
        path: '/pages/contentDetails/contentDetails?UserId=' + UserId + '&ProductId=' + this.ProductId
      }
    }
  },
  computed: {
    isOpenid () {
      this.phoneNumber = uni.getStorageSync('phoneNumber')
      this.openid = uni.getStorageSync('openid')
      if (this.openid == '') {
        return true
      }
      return false
    },
    isUserId () {
      if (uni.getStorageSync('UserId')) {
        return true
      }
      return false
    }
  },
  onLoad (options) {
    this.ProductId = options.ProductId
    if (options.UserId) {
      uni.setStorageSync('ReferralUserId', options.UserId)
    }
    // if (this.ProductId != undefined) {
    // 获取详情内容
    this.GetProductByID()
    // 获取行程介绍的内容
    this.GetProductTripByProductID()
    // }
  }
}
</script>

<style>
/* 头部照片区域 */
.banner {
  background-color: #fff;
  margin-bottom: 16rpx;
}

.banner image {
  height: 400rpx;
  width: 100%;
}

.banner-content {
  padding: 0 32rpx 24rpx 32rpx;
}

.banner-title {
  font-size: 36rpx;
  color: #525252;
  text-overflow: -o-ellipsis-lastline;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  line-clamp: 2;
  -webkit-box-orient: vertical;
}

.banner-price {
  font-size: 40rpx;
  color: #f0c462;
  margin-top: 10rpx;
}

/* 订单相关信息 */
.order-box {
  width: 100%;
  margin-bottom: 16rpx;
  background-color: #fff;
  box-sizing: border-box;
  padding: 26rpx 48rpx 24rpx;
}

.order-box view {
  font-size: 24rpx;
  color: #525252;
  margin: 7rpx 0;
}

.order-box text {
  font-size: 24rpx;
  color: #525252;
  margin-left: 10rpx;
}

/* 线路特色区域 */
.characteristic {
  background-color: #fff;
  padding: 22rpx 50rpx;
  box-sizing: border-box;
  margin-bottom: 16rpx;
}

.characteristic-title {
  font-size: 30rpx;
  color: #373737;
  text-align: center;
}

/* 行程介绍区域 */
.introduce {
  padding: 22rpx 50rpx;
  background-color: #fff;
  margin-bottom: 16rpx;
}

.introduce-title {
  font-size: 30rpx;
  color: #373737;
  text-align: center;
  margin-bottom: 10rpx;
}

.introduce-text {
  font-size: 24rpx;
  color: #373737;
  text-align: center;
}

.introduce-content {
  font-size: 28rpx;
  color: #797979;
  margin-bottom: 40rpx;
}

.introduce-content view {
  margin: 8rpx;
}

.place {
  color: #4eb4a0;
}

/* 费用介绍 */
.cost {
  padding: 22rpx 50rpx;
  background-color: #fff;
  margin-bottom: 16rpx;
}

.cost-title {
  font-size: 30rpx;
  text-align: center;
}

.cost-contain {
  color: #4eb4a0;
  font-size: 28rpx;
}

.cost-content {
  font-size: 28rpx;
  color: #797979;
}

.cost-content view {
  margin: 10rpx 0;
}

.cost-tips {
  font-size: 28rpx;
  color: #4d4d4d;
}

.cost-tips text {
  font-size: 28rpx;
  color: #797979;
}

/* 购买须知区域 */
.notice {
  padding: 22rpx 50rpx;
  background-color: #fff;
  margin-bottom: 16rpx;
}

.notice-title {
  font-size: 30rpx;
  text-align: center;
}

.guarantee {
  height: 56rpx;
  display: flex;
  justify-content: center;
  align-items: center;
}

.guarantee image {
  width: 30rpx;
  height: 30rpx;
  margin-right: 10rpx;
}

.guarantee view {
  font-size: 20rpx;
  color: #4eb4a0;
}

/* 固定定位区域 */
.location-copy {
  width: 100%;
  height: 98rpx;
}

.location {
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 98rpx;
  line-height: 98rpx;
  display: flex;
  background-color: #fff;
  border-top: 1rpx solid #eee;
}

.location-one {
  width: 316rpx;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

.location-one image {
  width: 46rpx;
  height: 46rpx;
}

.location-one > view {
  font-size: 20rpx;
  color: #737c84;
}

.location-two {
  text-align: center;
  width: 434rpx;
  font-size: 40rpx;
  color: #fff;
  background-color: #f0c462;
  padding: 0;
  border-radius: 0;
}

.location-two::after {
  width: 0;
  height: 0;
}

/* 弹出层区域 */
.box {
  width: 448rpx;
  height: 300rpx;
  background-color: #fff;
  border-radius: 20rpx;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.box-title {
  margin-top: 30rpx;
  font-size: 28rpx;
  color: #000;
  font-weight: 500;
}

.box-content {
  font-size: 28rpx;
  color: #acacac;
}

.box-footer {
  font-size: 28rpx;
  color: #5e6c96;
  font-weight: 500;
  height: 84rpx;
  line-height: 84rpx;
  border-top: 1rpx solid #ccc;
}

.common {
  text-align: center;
}
.share-button {
  position: fixed;
  top: 30%;
  right: 10%;
}
.btn {
  width: 60rpx;
  height: 60rpx;
  padding: 0;
}
.img {
  width: 100%;
  height: 100%;
}
.btn::after {
  width: 0;
  height: 0;
}
</style>