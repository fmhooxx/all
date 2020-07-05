<template>
  <!-- 支付订单页面 -->
  <view>
    <view class="head">
      <view>应付金额</view>
      <view class="num">¥{{Amount}}</view>
    </view>
    <view class="footer"
          @click="goPaymentResult">微信支付</view>
  </view>
</template>

<script>
export default {
  data () {
    return {
      // 支付凭证
      PayVoucherNumber: '',
      // 订单总额
      Amount: ''
    }
  },
  methods: {
    // 去支付结果页面
    goPaymentResult () {
      this.$http.post('/api/WeiXinPay.ashx', {
        action: 'Pay',
        voucherNumber: this.PayVoucherNumber,
        OpenId: uni.getStorageSync('openid')
      }).then(res => {
        uni.requestPayment({
          provider: 'wxpay',
          timeStamp: res.data.timeStamp,
          nonceStr: res.data.nonceStr,
          package: 'prepay_id=' + res.data.prepay_id,
          signType: 'MD5',
          paySign: res.data.paySign,
          success: (res) => {
            console.log(res)
            if (res.errMsg == 'requestPayment:ok') {
              uni.reLaunch({
                url: '/pages/paymentResult/paymentResult'
              })
            } else {
              console.log('支付失败')
            }
          },
          fail: (err) => {
            uni.showToast({
              title: '支付失败',
              duration: 2000,
              icon: 'none',
              mask: true,
              success: () => {
                setTimeout(() => {
                  uni.reLaunch({
                    url: '/pages/orderList/orderList?active=' + 0
                  })
                }, 1500)
              }
            });
          }
        });
      })
    }
  },
  onLoad (options) {
    this.PayVoucherNumber = options.PayVoucherNumber
    this.Amount = options.Amount
  }
}
</script>

<style>
.head {
  width: 100%;
  height: 228rpx;
  padding-top: 60rpx;
  text-align: center;
  background-color: #fff;
  box-sizing: border-box;
}

.num {
  margin-top: 20rpx;
}

.head view {
  font-size: 40rpx;
  color: #525252;
}

.footer {
  margin: 20rpx auto;
  font-size: 40rpx;
  color: #fff;
  width: 690rpx;
  height: 85rpx;
  line-height: 85rpx;
  text-align: center;
  background-color: #f0c462;
}
</style>