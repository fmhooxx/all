<template>
	<view>
		<uni-calendar :insert="true" :lunar="true" :start-date="'startData'" :end-date="'2099-5-20'" @change="change">
		</uni-calendar>
	</view>
</template>

<script>
	import uniCalendar from '@/components/uni-calendar/uni-calendar.vue'
	export default {
		components: {
			uniCalendar
		},
		data() {
			return {

			}
		},
		methods: {
			change(e) {
				console.log(e)
			}
		}
	}
</script>

<style>
	.uni-numbox {
		width: 160rpx !important;
		height: 50rpx !important;
		line-height: 50rpx !important;
	}

	.uni-numbox view {
		width: 160rpx !important;
		height: 50rpx !important;
		line-height: 50rpx !important;
	}

	.uni-numbox__value {
		width: 160rpx !important;
		height: 50rpx !important;
		line-height: 50rpx !important;
		font-size: 26rpx !important;
	}

	.uni-numbox__plus .uni-numbox--text {
		color: #4eb4a0 !important;
	}
</style>