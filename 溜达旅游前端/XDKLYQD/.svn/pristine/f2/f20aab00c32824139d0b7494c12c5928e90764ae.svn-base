<template>
  <view>
    <uniPopup ref="popup"
              type="center">
      <view class="popup">
        <view class="popup-title">您还未登录</view>
        <view class="popup-text">登录后可享受完整服务</view>
        <view class="popup-img">
          <image src="/static/images/logo1.jpg"></image>
        </view>
        <view class="popup-content">
          <view @click="loginClose">暂不登录</view>
          <button class="btn"
                  open-type="getUserInfo"
                  @getuserinfo="goLogin">
            立即登录
          </button>
        </view>
      </view>
    </uniPopup>
  </view>
</template>

<script>
import uniPopup from '@/components/uni-popup/uni-popup.vue'
export default {
  components: {
    uniPopup,
  },
  data () {
    return {}
  },
  methods: {
    // 打开弹窗
    loginOpen () {
      this.$refs.popup.open()
    },
    // 关闭弹窗
    loginClose () {
      this.$refs.popup.close()
    },
    // 登录
    goLogin () {
      uni.login({
        provider: 'weixin',
        success: (res) => {
          var code = res.code
          this.$http
            .post('/api/WeiXinApplet.ashx', {
              action: 'Login',
              code: code,
              ReferralUserId: uni.getStorageSync('ReferralUserId')
            })
            .then((res) => {
              console.log(res)
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
                  icon: 'none',
                })
              }
            })
        },
      })
    },
    getUser () {
      uni.getUserInfo({
        provider: 'weixin',
        success: (res) => {
          console.log(res)
          if (res.errMsg == 'getUserInfo:ok') {
            uni.setStorageSync('avatarUrl', res.userInfo.avatarUrl)
            uni.setStorageSync('nickName', res.userInfo.nickName)
            this.$http
              .post('/api/WeiXinApplet.ashx', {
                action: 'UserBindInfo',
                UserId: uni.getStorageSync('UserId'),
                nickName: res.userInfo.nickName,
                gender: res.userInfo.gender,
                avatarUrl: res.userInfo.avatarUrl,
              })
              .then((res) => {
                console.log(res)
                if (res.data.status == 'true') {
                  uni.navigateTo({
                    url: '/pages/login/login',
                  })
                }
              })
          }
        },
      })
    },
  },
}
</script>

<style>
/* 登录的弹框 */
.popup {
  /* width: 500rpx;
		height: 550rpx; */
  width: 440rpx;
  height: 465rpx;
  border-radius: 10rpx;
  background-color: #fff;
  padding: 34rpx 33rpx;
  box-sizing: border-box;
}

.popup view {
  text-align: center;
}

.popup-img {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 25rpx;
}

.popup-img image {
  width: 180rpx;
  height: 180rpx;
  border-radius: 50%;
}

.popup-title {
  font-size: 30rpx;
  color: #3b3b3b;
}

.popup-text {
  font-size: 26rpx;
  color: #a0a0a0;
  margin: 20rpx 0 40rpx 0;
}

.popup-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.btn {
  padding: 0;
  line-height: 58rpx;
  color: #fff;
  background-color: #4eb4a0;
  font-size: 30rpx;
  width: 160rpx;
  height: 58rpx;
  line-height: 58rpx;
  text-align: center;
  border-radius: 30rpx;
  border: 1rpx solid #4eb4a0;
}

.btn::after {
  width: 0;
  height: 0;
}

.popup-content :nth-child(1) {
  color: #626262;
  background-color: #fff;
  font-size: 30rpx;
  width: 160rpx;
  height: 58rpx;
  line-height: 58rpx;
  text-align: center;
  border-radius: 30rpx;
  border: 1rpx solid #d7d7d7;
}
</style>
