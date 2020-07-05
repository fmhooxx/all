<template>
	<!-- 修改密码页面 -->
	<view>
		<view class="head">
			<input placeholder="请输入旧的密码" placeholder-class="password" v-model="usedPassword" />
			<image @click="usedRemove" v-if="isUsedInput" src="/static/images/quxiao.png"></image>
		</view>
		<view class="head">
			<input placeholder="请输入新的密码" placeholder-class="password" v-model="password" />
			<image @click="remove" v-if="isInput" src="/static/images/quxiao.png"></image>
		</view>
		<view class="success" @click="complete">完成</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 输入的旧密码
				usedPassword: '',
				// 输入的新密码
				password: ''
			}
		},
		methods: {
			// 清除旧密码输入框里的内容
			usedRemove() {
				this.usedPassword = ''
			},
			// 清除新密码输入框里的内容
			remove() {
				this.password = ''
			},
			// 返回个人中心页面
			complete() {
				uni.showModal({
					content: '修改密码成功',
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
			isUsedInput() {
				if (this.usedPassword == '') {
					return false
				}
				return true
			},
			isInput() {
				if (this.password == '') {
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

	.password {
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