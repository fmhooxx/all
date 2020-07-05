<template>
  <!-- 首页页面 -->
  <view>
    <!-- 轮播图区域 -->
    <view class="banner">
      <swiper indicator-dots
              indicator-color="rgba(255,255,255)"
              indicator-active-color="#8ed0a2"
              autoplay
              circular>
        <block v-for="(item, index) in swiperImg"
               :key="index">
          <swiper-item>
            <image :src="item"></image>
          </swiper-item>
        </block>
      </swiper>
    </view>
    <!-- 图文区域 -->
    <view class="content">
      <view class="img-box"
            @click="goContentDetails(item.ProductId)"
            v-for="(item, index) in list"
            :key="index">
        <image class="content-img"
               :src="item.ImageUrl1"></image>
        <view class="content-content">
          <view class="content-title">{{item.ProductName}}</view>
          <view class="content-footer">{{item.ShortDescription}}</view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data () {
    return {
      // 首页数据
      list: [],
      swiperImg: [
        '../../static/images/index-1.jpg',
        '../../static/images/index-2.jpg',
        '../../static/images/index-3.jpg',
        '../../static/images/index-4.png',
        '../../static/images/index-5.jpg',
        '../../static/images/index-6.jpg'
      ]
    };
  },
  methods: {
    GetProductListByPage () {
      this.$http.post('/api/WeiXinApplet.ashx', {
        action: "GetProductListByPage",
        keywords: '',
        productCode: '',
        // 类别 1 代表旅游 2 代表捕鱼 4 代表海钓 
        categoryIds: '1',
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
          console.log(this.list)
        } else {
          uni.showToast({
            title: '网络错误, 请稍后重试',
            duration: 2000,
            mask: true
          });
        }
      })
    },
    // 去图文详情页面
    goContentDetails (id) {
      uni.navigateTo({
        url: "/pages/contentDetails/contentDetails?ProductId=" + id
      });
    }
  },
  onLoad () {
    // 根据类别获取页面数据
    this.GetProductListByPage()
  }
};
</script>

<style>
page {
  background-color: #f9f9f9;
}

/* 轮播图区域 */
.banner {
  padding: 0 30rpx;
}

.banner swiper {
  height: 400rpx;
}

.banner image {
  width: 100%;
  height: 100%;
  border-radius: 10rpx;
}

.img-box {
  margin: 22rpx auto 0;
  width: 700rpx;
  height: 500rpx;
  border-radius: 10rpx;
  /* background-color: green; */
  box-shadow: 0 9rpx 16rpx 0 rgba(234, 234, 234, 0.5);
}

/* 图文区域 */
.content-img {
  height: 344rpx;
  width: 100%;
  border-radius: 10rpx 10rpx 0 0;
}

.content-content {
  margin-left: 20rpx;
}

.content-title {
  font-size: 40rpx;
  color: #525252;
  margin: 16rpx 0 8rpx 0;
  white-space: nowrap;
  /*一行显示*/
  overflow: hidden;
  /*超出部分隐藏*/
  text-overflow: ellipsis;
}

.content-footer {
  font-size: 22rpx;
  color: #737c84;
  white-space: nowrap;
  /*一行显示*/
  overflow: hidden;
  /*超出部分隐藏*/
  text-overflow: ellipsis;
}
</style>