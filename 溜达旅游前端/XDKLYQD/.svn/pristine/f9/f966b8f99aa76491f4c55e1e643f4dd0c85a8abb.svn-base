<template>
  <view>
    <!-- 预订人信息区域 -->
    <view class="reserve">
      <view class="reserve-title">预订人信息</view>
      <view>
        <view class="reserve-content">
          <view>公司名</view>
          <input placeholder="请输入公司名"
                 placeholder-class="placeholder-common"
                 v-model="companyName" />
        </view>
        <view class="reserve-content">
          <view>姓名</view>
          <input placeholder="请输入姓名"
                 placeholder-class="placeholder-common"
                 v-model="uname" />
        </view>
        <view class="reserve-content">
          <view>手机号</view>
          <input placeholder="请输入手机号"
                 placeholder-class="placeholder-common"
                 v-model="phone" />
        </view>
        <view class="reserve-content">
          <view>验证码</view>
          <view class="code-box">
            <input placeholder="验证码"
                   placeholder-class="placeholder-common"
                   v-model="code" />
            <view v-if="isLogin"
                  class="code-common code"
                  @click="getCode">获取验证码</view>
            <view v-else
                  class="code-common code-num">{{ num }}秒后重新获取</view>
          </view>
        </view>
      </view>
    </view>
    <!-- 电话区域 -->
    <view style="margin-top: 20rpx;">
      <view class="common tel"
            @click="goMakePhoneCall">请联系VIP客服</view>
    </view>
    <view class="shelter"></view>
    <view class="next"
          @click="goConfirmationOrder"><span>订金: ¥500</span>支付</view>
  </view>
</template>

<script>
export default {
  data () {
    return {
      // 控制发送以及剩余时间的切换显示
      isLogin: true,
      // 定时器命名
      timer: "",
      // 倒计时内容
      num: 60,
      // 公司名称
      companyName: '',
      // 姓名
      uname: '',
      // 电话
      phone: '',
    }
  },
  methods: {
    // 去确认订单页面
    goConfirmationOrder () {
      if (this.companyName != '' && this.uname != '' && this.phone.length == 11) {
        uni.showToast({
          title: '通过',
          duration: 2000,
          icon: 'none',
          mask: true
        });
      } else if (this.companyName == '') {
        uni.showToast({
          title: '公司名不能为空',
          duration: 2000,
          icon: 'none',
          mask: true
        });
      } else if (this.uname == '') {
        uni.showToast({
          title: '姓名不能为空',
          duration: 2000,
          icon: 'none',
          mask: true
        });
      } else if (this.phone.length != 11) {
        uni.showToast({
          title: '请输入十一位的手机号码',
          duration: 2000,
          icon: 'none',
          mask: true
        });
      }
      // uni.navigateTo({
      //   url: '/pages/confirmationOrder/confirmationOrder'
      // })
    },
    // 获取验证码
    getCode () {
      this.isLogin = false
      this.countDown()
    },
    // 倒计时效果
    countDown () {
      // 获取倒计时的初始值
      var time = this.num;
      // 为定时器命名
      this.timer = setInterval(() => {
        // 每隔一秒 num 就减一 实现同步
        time--;
        // 然后把 num 存进 data, 让用户知道时间在倒记着
        this.num = time;
        if (time == 0) {
          clearInterval(this.timer);
          // 当时间为 0 的时候 隐藏定时器的内容 显示发送的内容 并且为定时器重新赋值
          this.isLogin = true;
          this.num = 60;
        }
      }, 1000);
    },
    // 拨打号码
    goMakePhoneCall () {
      uni.makePhoneCall({
        phoneNumber: '17855355076' //仅为示例
      });
    }
  }
}
</script>

<style>
/* 预订人信息区域 */
.reserve {
  box-sizing: border-box;
  padding: 30rpx;
  background-color: #fff;
}

.reserve-title {
  font-size: 36rpx;
  color: #545454;
}

.reserve-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 20rpx 0;
}

.reserve-content > input {
  width: 81%;
  padding: 8rpx;
  font-size: 26rpx;
  color: #525252;
  border: 1rpx solid #e5e5e5;
}

.reserve-content view {
  font-size: 26rpx;
  color: #525252;
}

/* 电话区域 */
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
/* 验证码区域 */
.code-box {
  width: 81%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1rpx solid #e5e5e5;
  padding: 8rpx;
}
.code-box view {
  font-size: 26rpx;
  color: #525252;
}
.code-box .code-common {
  width: 174rpx;
  height: 48rpx;
  line-height: 48rpx;
  text-align: center;
  font-size: 22rpx;
}
.code-box .code {
  color: #fff;
  background-color: #4eb4a0;
}
.code-box .code-num {
  color: #4eb4a0;
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
.next span {
  margin-right: 20rpx;
}

.shelter {
  width: 100%;
  height: 98rpx;
}
</style>