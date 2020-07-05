<template>
	<!-- 支付结果页面 -->
	<view>
		<view class="success">支付成功</view>
		<view class="footer">
			<view class="one" @click="goRecommend">继续逛逛</view>
			<view class="two" @click="goOrderList">查看订单</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {
			// 去推荐页面
			goRecommend() {
				uni.switchTab({
					url: '/pages/recommend/recommend'
				});
			},
			// 去订单列表页面
			goOrderList() {
				uni.redirectTo({
					url: '/pages/orderList/orderList'
				});
			}
		}
	}
</script>

<style>
	.success {
		width: 100%;
		height: 358rpx;
		line-height: 358rpx;
		text-align: center;
		font-size: #3f3f3f;
		font-size: 40rpx;
		background-color: #fff;
		margin-bottom: 110rpx;
	}

	.footer {
		display: flex;
		justify-content: space-evenly;
	}

	.footer view {
		font-size: 36rpx;
		width: 300rpx;
		height: 85rpx;
		line-height: 85rpx;
		text-align: center;
		color: #fff;
	}

	.one {
		background-color: #f0c462;
	}

	.two {
		background-color: #afafaf;
	}
</style>