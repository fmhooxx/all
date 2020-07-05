<template>
  <!-- 登录页面 -->
  <view class="login">
    <view class="logo">
      <image src="../../static/images/logo.jpg"></image>
      <view>雄登康旅游</view>
    </view>
    <view class="content"></view>
    <!-- <button class="btn common" open-type="getPhoneNumber" @click="getPhoneNumber"> -->
    <!-- #ifdef MP-WEIXIN -->
    <button class="btn common"
            open-type="getPhoneNumber"
            @getphonenumber="getPhoneNumber">
      <!-- #endif -->
      <image src="../../static/images/white-weixin.png"></image>
      使用微信授权登录
      <!-- </button> -->
    </button>
    <button class="common code"
            @click="open">短信验证码登录</button>
    <!-- 弹出层区域 -->
    <uniPopup ref="popup"
              type="bottom">
      <view class="box">
        <view class="box-title">短信验证码登录</view>
        <view class="box-content">若手机号未注册，验证后将自动注册</view>
        <view class="box-common">
          <view class="common-text">手机号</view>
          <input type="number"
                 v-model="phone"
                 placeholder="请输入手机号" />
        </view>
        <view class="box-common">
          <view class="code-box">
            <view class="common-text">验证码</view>
            <input type="number"
                   placeholder="请输入验证码"
                   v-model="code" />
          </view>
          <view class="box-code"
                v-if="isLogin"
                @click="getCode">获取验证码</view>
          <view class="num"
                v-else>{{ num }}秒后重新获取</view>
        </view>
        <button class="btn"
                @click="determine">登录</button>
      </view>
    </uniPopup>
  </view>
</template>

<script>
import uniPopup from "@/components/uni-popup/uni-popup.vue";
export default {
  components: {
    uniPopup
  },
  data () {
    return {
      // 控制发送以及剩余时间的切换显示
      isLogin: true,
      // 定时器命名
      timer: "",
      // 倒计时内容
      num: 60,
      // 输入的手机号码
      phone: null,
      // 输入的验证码
      code: null,
      // 收到的短信验证码
      receivedCode: null,
      // 传递过来的 页面详情的 id
      ProductId: ''
    };
  },
  methods: {
    // 点击获取验证码
    getCode () {
      // 调用定时器
      this.countDown();
      // 手机号码的正则表达式
      var reg =
        /^(((13[0-9]{1})|(15[0-9]{1})|(16[0-9]{1})|(17[3-8]{1})|(18[0-9]{1})|(19[0-9]{1})|(14[5-7]{1}))+\d{8})$/;
      if (reg.test(this.phone)) {
        this.isLogin = false;
        this.$http
          .post("/api/WeiXinApplet.ashx", {
            action: "GetCode",
            phone: this.phone
          })
          .then(res => {
            console.log(res);
            if (res.data.status == 'true') {
              uni.setStorageSync('phoneNumber', this.phone)
              this.receivedCode = res.data.code
            } else {
              uni.showToast({
                title: '今日已获取最大短信条数限制，请明日再试',
                duration: 2000,
                icon: 'none'
              });
            }
          });
      } else {
        uni.showToast({
          title: '请输入正确的手机号码',
          duration: 2000,
          icon: 'none'
        });
      }
    },
    // 验证码获取到后 点击登录
    determine () {
      if (this.code == this.receivedCode) {
        this.$http.post('/api/WeiXinApplet.ashx', {
          action: 'PhoneLogin',
          UserId: uni.getStorageSync('UserId'),
          phone: this.phone,
          code: this.code
        }).then(res => {
          console.log(res)
          if (res.data.status == 'true') {
            if (this.ProductId == undefined) {
              uni.switchTab({
                url: '/pages/me/me'
              });
            } else {
              uni.reLaunch({
                url: '/pages/contentDetails/contentDetails?ProductId=' + this.ProductId
              })
            }
          }
        })
      } else {
        uni.showToast({
          title: '您输入的验证码不正确',
          duration: 2000,
          icon: 'none'
        });
      }
    },
    // 打开遮罩层
    open () {
      this.$refs.popup.open();
    },
    // 获取用户手机号码 先判断用户登录状态是否过期 如果过期 就需要重新获取
    getPhoneNumber (e) {
      var msg = e.detail.errMsg
      var encryptedData = e.detail.encryptedData
      var session_key = uni.getStorageSync('session_key')
      var iv = e.detail.iv
      if (msg == 'getPhoneNumber:ok') {
        // 检查用户登录状态
        uni.checkSession({
          success: () => {
            // 获取手机号码
            this.deciyption(session_key, encryptedData, iv)
          },
          fail: () => {
            uni.login({
              provider: 'weixin',
              success: (res) => {
                var code = res.code
                this.$http.post('/api/WeiXinApplet.ashx', {
                  action: "Login",
                  code: code,
                  ReferralUserId: uni.getStorageSync('ReferralUserId')
                }).then(res => {
                  console.log(res)
                  if (res.data.status == 'true') {
                    uni.setStorageSync('openid', res.data.openid)
                    uni.setStorageSync('session_key', res.data.session_key)
                    uni.setStorageSync('UserId', res.data.UserId)
                    this.deciyption(res.data.session_key, encryptedData, iv);
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
          }
        })
      }
    },
    // 获取用户手机号码
    deciyption (session_key, encryptedData, iv) {
      this.$http.post('/api/WeiXinApplet.ashx', {
        action: 'GetPhoneNumber',
        session_key: session_key,
        encryptedData: encryptedData,
        iv: iv,
        UserId: uni.getStorageSync('UserId')
      }).then(res => {
        console.log(res)
        if (res.data.status == 'true') {
          uni.setStorageSync('phoneNumber', res.data.phoneNumber)
          if (this.ProductId == undefined) {
            uni.switchTab({
              url: '/pages/me/me'
            });
          } else {
            uni.reLaunch({
              url: '/pages/contentDetails/contentDetails?ProductId=' + this.ProductId
            })
          }
        }
      })
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
    }
  },
  onLoad (options) {
    this.ProductId = options.ProductId
    // console.log(this.ProductId)
  }
};
</script>

<style>
image {
  width: 100%;
  height: 40rpx;
}

.login {
  position: relative;
}

.logo {
  position: absolute;
  top: 50rpx;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.logo > image {
  width: 130rpx;
  height: 130rpx;
  border-radius: 20rpx;
}

.logo view {
  font-size: 32rpx;
  color: #4eb4a0;
  margin-top: 20rpx;
}

.content {
  width: 100%;
  height: 350rpx;
}

.btn > image {
  width: 40rpx;
  height: 40rppx;
  margin-right: 20rpx;
}

.common {
  height: 100rpx;
  line-height: 100rpx;
  font-size: 32rpx;
  width: 690rpx;
}

.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #4eb4a0;
  color: #fff;
}

.code {
  color: #4eb4a0;
  border: 1rpx solid #4eb4a0;
  margin-top: 40rpx;
}

/* 弹出层区域 */
.box {
  padding-bottom: 20rpx;
  height: 955rpx;
  width: 100%;
  background-color: #fff;
  border-radius: 20rpx 20rpx 0 0;
}

.box-title {
  font-size: 40rpx;
  font-weight: 500;
  color: #363636;
  padding-top: 40rpx;
  text-align: center;
}

.box-content {
  font-size: 28rpx;
  color: #363636;
  margin: 40rpx 0 80rpx 0;
  text-align: center;
}

.box-common {
  display: flex;
  border-bottom: 2rpx solid #f3f3f3;
  padding: 20rpx;
}

.common-text {
  font-size: 40rpx;
  color: #363636;
  margin-right: 20rpx;
  width: 127rpx;
}

.code-box {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.box-code {
  height: 48rpx;
  line-height: 48rpx;
  text-align: center;
  width: 174rpx;
  font-size: 22rpx;
  background-color: #4eb4a0;
  color: #fff;
}

.num {
  width: 174rpx;
  height: 48rpx;
  line-height: 48rpx;
  text-align: center;
  font-size: 22rpx;
  color: #4eb4a0;
}

.btn {
  margin-top: 40rpx;
  width: 690rpx;
  height: 85rpx;
  font-size: 32rpx;
  background-color: #4eb4a0;
  color: #fff;
}
</style>