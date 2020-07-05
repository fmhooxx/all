<template>
  <!-- 选择出行时间/人数页面 -->
  <view>
    <!-- 日历区域 -->
    <view>
      <uni-calendar :insert="true"
                    :lunar="true"
                    :start-date="'startData'"
                    :end-date="endData"
                    :showMonth="false"
                    @change="change"
                    :selected="selected">
      </uni-calendar>
    </view>
    <!-- 人数区域 -->
    <view class="people">
      <view class="common">请选择出行人数<text class="warning">(带红点的是可选择的时间)</text></view>
      <view class="common people-content">
        <view class="people-num">
          <view class="people-class">成人</view>
          <uniNumberBox value="1"
                        :min="0"
                        :max="9999"
                        @change="adultChange"></uniNumberBox>
        </view>
        <view class="people-num children">
          <view class="people-class">儿童</view>
          <uniNumberBox value="0"
                        :min="0"
                        :max="9999"
                        @change="childrenChange"></uniNumberBox>
        </view>
      </view>
      <view class="footer">
        <image src="/static/images/mark.png"></image>
        <view>12周岁以下为儿童</view>
      </view>
    </view>
    <view class="next"
          @click="goFillOrder">下一步</view>
  </view>
</template>

<script>
import { GetOrderAmount } from '../api/agreement'
import uniCalendar from "@/components/uni-calendar/uni-calendar.vue";
import uniNumberBox from "@/components/uni-number-box/uni-number-box.vue";
export default {
  components: {
    uniCalendar,
    uniNumberBox
  },
  data () {
    return {
      // 日历的开始日期
      startData: '',
      endData: '2099-12-29',
      // 成人人数
      adultNum: 0,
      // 儿童人数
      childrenNum: 0,
      // 选择的日期
      fulldate: '',
      // 页面传递过来的 id 值
      ProductId: '',
      // 红点日期
      selected: '',
      // 支付金额
      MaxShowPrice: ''
    };
  },
  methods: {
    // 当日期发生改变的时候
    change (e) {
      var data = e.fulldate
      for (var i = 0; i < this.selected.length; i++) {
        var choice = this.selected[i].date
        // console.log(choice)
        if (data == choice) {
          this.fulldate = choice
          return
        }
      }
      for (var i = 0; i < this.selected.length; i++) {
        var choice = this.selected[i].date
        if (data !== choice) {
          this.fulldate = ''
          uni.showToast({
            title: '请选择带有红点的日期',
            duration: 2000,
            icon: 'none',
            mask: true
          });
          return
        }
      }
    },
    // 成人输入框内容发生变化的时候
    adultChange (e) {
      this.adultNum = parseInt(e)
    },
    // 儿童输入框内容发生变化的时候
    childrenChange (e) {
      this.childrenNum = parseInt(e)
    },
    // 去填写订单信息页面
    goFillOrder () {
      this.choiceTimeNum()
    },
    // 选择出行时间和人数
    choiceTimeNum () {
      var total = this.adultNum + this.childrenNum
      if (total < 10 && this.fulldate) {
        var result = {
          action: 'GetOrderAmount',
          userID: uni.getStorageSync('UserId'),
          maxUserCount: this.adultNum,
          minUserCount: this.childrenNum,
          productID: this.ProductId,
        }
        GetOrderAmount(result).then(res => {
          console.log(res)
          var amountTotal = res.data.amountTotal
          if (res.data.status == 'true') {
            uni.navigateTo({
              url: '/pages/fillOrder/fillOrder?adultNum=' + this.adultNum + '&childrenNum=' + this.childrenNum + '&ProductId=' + this.ProductId + '&fulldate=' + this.fulldate + '&amountTotal=' + amountTotal
            });
          }
        })
      } else if (total >= 10 && this.fulldate) {
        uni.navigateTo({
          url: '/pages/company/company'
        });
      } else {
        uni.showToast({
          title: '请选择带有红点的日期',
          duration: 2000,
          icon: 'none'
        });
      }
    },
    // 获取当前日期
    getTime () {
      var date = new Date(),
        year = date.getFullYear(),
        month = date.getMonth() + 1,
        day = date.getDate(),
        hour = date.getHours() < 10 ? "0" + date.getHours() : date.getHours(),
        minute = date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes(),
        second = date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds();
      month >= 1 && month <= 9 ? (month = "0" + month) : "";
      day >= 0 && day <= 9 ? (day = "0" + day) : "";
      var timer = year + '-' + month + '-' + day
      this.startData = timer
      return timer;
    },
    // 获取出发时间
    GetProductOpenDateByProductID () {
      this.$http.post('/api/WeiXinApplet.ashx', {
        action: 'GetProductOpenDateByProductID',
        productId: this.ProductId
      }).then(res => {
        // console.log(res)
        if (res.data.status == true) {
          var result = []
          for (var i = 0; i < res.data.Data.Data.length; i++) {
            var str = {
              date: res.data.Data.Data[i].OpenDate
            }
            result.push(str)
          }
          this.selected = result
        }
      })
    }
  },
  onShow () {
    this.getTime()
  },
  onLoad (options) {
    this.ProductId = options.productId
    if (this.ProductId != undefined) {
      // 获取出发时间
      this.GetProductOpenDateByProductID()
    }
    this.MaxShowPrice = options.MaxShowPrice
  }
};
</script>

<style>
/* 人数区域 */
.people {
  margin-top: 30rpx;
  margin-left: 40rpx;
}

.common {
  height: 98rpx;
  line-height: 98rpx;
  width: 100%;
  border-bottom: 1rpx solid #e8e8e8;
}

.warning {
  color: red;
}

.people-num {
  display: flex;
  align-items: center;
}

.people-content {
  display: flex;
}

.people-class {
  font-size: 26rpx;
  color: #545454;
  margin-right: 20rpx;
}

.children {
  margin-left: 40rpx;
}

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

.footer {
  display: flex;
  height: 60rpx;
  align-items: center;
  border-bottom: 1rpx solid #e8e8e8;
}

.footer view {
  margin-left: 10rpx;
  font-size: 22rpx;
  color: red;
}

.footer image {
  width: 25rpx;
  height: 25rpx;
}

.next {
  position: absolute;
  bottom: 0;
  height: 98rpx;
  line-height: 98rpx;
  text-align: center;
  width: 100%;
  font-size: 36rpx;
  background-color: #f0c462;
  color: #fff;
}
</style>