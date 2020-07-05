<template>
  <!-- 设置页面 -->
  <view class="set-up">
    <!-- <view class="common" @click="goNickname">
			<view>用户名称</view>
			<image src="../../static/images/right-arrow.png"></image>
		</view>
		<view class="common" @click="goChangePassword">
			<view>修改密码</view>
			<image src="../../static/images/right-arrow.png"></image>
		</view> -->
    <view class="common"
          @click="goFeedback">
      <view>意见反馈</view>
      <image src="../../static/images/right-arrow.png"></image>
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
    // 去用户昵称页面
    goNickname () {
      uni.navigateTo({
        url: '/pages/nickName/nickName'
      });
    },
    // 去修改密码页面
    goChangePassword () {
      uni.navigateTo({
        url: '/pages/changePassword/changePassword'
      });
    },
    // 去意见反馈页面
    goFeedback () {
      uni.navigateTo({
        url: '/pages/feedback/feedback'
      });
    }
  }
}
</script>

<style>
.set-up {
  margin-top: 8rpx;
}

.common {
  height: 96rpx;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
  padding: 0 34rpx;
  margin-bottom: 4rpx;
}

.common view {
  color: #545454;
  font-size: 34rpx;
}

.common image {
  width: 20rpx;
  height: 30rpx;
}
</style>