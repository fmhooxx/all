<template>
	<!-- 用户昵称页面 -->
	<view>
		<view class="head">
			<input placeholder="请输入新的昵称" placeholder-class="uname" v-model="uname" />
			<image @click="remove" v-if="isInput" src="/static/images/quxiao.png"></image>
		</view>
		<view class="success" @click="complete">完成</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 输入的昵称
				uname: ''
			}
		},
		methods: {
			// 清除输入框里的内容
			remove() {
				this.uname = ''
			},
			// 返回个人中心页面
			complete() {
				uni.showModal({
					content: '用户名已更新',
					showCancel: false,
					confirmText: '返回',
					confirmColor: '#59b9a6',
					success: (res) => {
						if (res.confirm) {
							uni.switchTab({
								url: '/pages/me/me'
							});
						}
					}
				});
			}
		},
		computed: {
			isInput() {
				if (this.uname == '') {
					return false
				}
				return true
			}
		},
	}
</script>

<style>
	.head {
		margin-top: 8rpx;
		height: 96rpx;
		width: 100%;
		display: flex;
		justify-content: space-between;
		align-items: center;
		box-sizing: border-box;
		padding: 0 28rpx;
		background-color: #fff;
	}

	.head input {
		width: 90%;
	}

	.head image {
		width: 40rpx;
		height: 40rpx;
	}

	.uname {
		font-size: 34rpx;
		color: #999;
	}

	.success {
		margin: 44rpx auto;
		width: 690rpx;
		height: 85rpx;
		line-height: 85rpx;
		text-align: center;
		color: #fff;
		background-color: #59b9a6;
	}
</style>