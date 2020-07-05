<template>
	<!-- 推荐页面 -->
	<view>
		<view class="list">
			<view class="list-item" @click="goContentDetails(item.ProductId)" v-for="(item, index) in list" :key="index">
				<image :src="item.ImageUrl1" mode="scaleToFill"></image>
				<view class="title">{{item.ProductName}}</view>
				<view class="content">{{item.ShortDescription}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {	
		data() {
			return {
				list: []
			}
		},
		methods: {
			GetProductListByPage() {
				this.$http.post('/api/WeiXinApplet.ashx', {
					action: "GetProductListByPage",
					keywords: '',
					productCode: '',
					// 类别 1 代表旅游 2 代表捕鱼 4 代表海钓 
					categoryIds: '2,4',
					brandId: '',
					typeId: '',
					tagId: '',
					pageIndex: '',
					pageSize: '',
					sortBy: '',
					sortOrder: '',
				}).then(res => {
					console.log(res)
					if (res.data.status == true) {
						this.list = res.data.Data.Data
					} else {
						uni.showToast({
							title: '网络错误, 请稍后重试',
							duration: 2000,
							mask: true
						});
					}
				})
			},
			goContentDetails(id) {
				uni.navigateTo({
					url: '/pages/contentDetails/contentDetails?ProductId=' + id
				});
			}
		},
		onLoad() {
			// 根据类别获取页面数据
			this.GetProductListByPage()
		}
	}
</script>

<style>
	.list-item {
		width: 696rpx;
		height: 480rpx;
		margin: 0 auto 20rpx;
		border-radius: 10rpx;
		background-color: #fff;
	}

	.list-item image {
		border-radius: 10rpx 10rpx 0 0;
		width: 696rpx;
		height: 353rpx;
	}

	.list-item view {
		white-space: nowrap;
		/*一行显示*/
		overflow: hidden;
		/*超出部分隐藏*/
		text-overflow: ellipsis;
		/*用...代替超出部分*/
	}

	.title {
		font-size: 36rpx;
		color: #525252;
		margin: 10rpx 0 10rpx 33rpx;
	}

	.content {
		font-size: 22rpx;
		color: #737C84;
		margin-left: 22rpx;
	}
</style>