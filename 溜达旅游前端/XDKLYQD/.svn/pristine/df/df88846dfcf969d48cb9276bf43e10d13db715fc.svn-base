<template>
  <!-- 推荐列表页面 -->
  <view>
    <view v-if="isFlag">
      <view class="recommend-head-box">
        <view class="recommend-head">
          <view>被推荐电话</view>
          <view>消费金额</view>
          <view>注册时间</view>
        </view>
      </view>
      <view class="recommend-copy"></view>
      <view class="recommend-box">
        <view class="content"
              v-for="(item, index) in recommendList"
              :key="index">
          <view>{{item.CellPhone}}</view>
          <view>¥{{item.Results}}</view>
          <view>{{item.CreateDate}}</view>
        </view>
      </view>
    </view>
    <view v-else
          class="footer">
      <image src="/static/images/chaxun.png"></image>
      <view>没有查询到相关信息</view>
    </view>
  </view>
</template>

<script>
import { GetReferralUserResultsByPage } from '../api/agreement'
export default {
  data () {
    return {
      // 推荐列表数据
      recommendList: [],
      page: {
        // 当前页码值
        pageIndex: 1,
        // 当前页显示的条数
        pageSize: 20
      },
      // 总的数据条数
      total: '',
      // 节流阀
      flag: true
    }
  },
  methods: {
    // 获取推荐列表
    getRecommend () {
      var result = {
        action: 'GetReferralUserResultsByPage',
        userID: uni.getStorageSync('UserId'),
        pageIndex: this.page.pageIndex,
        pageSize: this.page.pageSize
      }
      GetReferralUserResultsByPage(result).then(res => {
        console.log(res.data.Data.Data)
        if (res.data.status == true) {
          this.total = res.data.Data.TotalRecords
          res.data.Data.Data.forEach((item, index) => {
            item.CreateDate = item.CreateDate.split(' ')[0]
          })
          this.recommendList.push(...res.data.Data.Data)
          var result = this.recommendList.length
          if (this.total == result) {
            this.flag = false
          }
        }
      })
    },
    // 上拉加载更多
    onReachBottom () {
      this.page.pageIndex += 1
      if (this.flag) {
        this.getRecommend()
      } else {
        uni.showToast({
          title: '我是有底线的',
          duration: 2000,
          icon: 'none',
          duration: 2000,
        })
      }
    }
  },
  computed: {
    isFlag () {
      if (this.recommendList.length == 0) {
        return false
      }
      return true
    }
  },
  onLoad () {
    // 获取推荐列表
    this.getRecommend()
  }
}
</script>

<style>
.recommend-head-box {
  position: fixed;
  top: 0;
  width: 100%;
}
.recommend-head {
  height: 100rpx;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
}
.recommend-copy {
  height: 100rpx;
  width: 100%;
}
.recommend-head > view {
  width: 33.33%;
  text-align: center;
  color: #4eb4a0;
  font-size: 28rpx;
}
.recommend-box {
  background-color: #fff;
  margin-top: 20rpx;
}
.content {
  height: 100rpx;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.content > view {
  width: 33.33%;
  text-align: center;
  font-size: 26rpx;
  color: #7d7d7f;
}
/* 无内容区域 */
/* 无内容区域 */
.footer {
  margin-top: 200rpx;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.footer image {
  width: 84rpx;
  height: 84rpx;
}

.footer view {
  margin-top: 40rpx;
  font-size: 28rpx;
  color: #545454;
}
</style>
