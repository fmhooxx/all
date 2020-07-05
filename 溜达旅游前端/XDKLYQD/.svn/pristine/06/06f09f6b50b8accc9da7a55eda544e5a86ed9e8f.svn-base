<template>
  <!-- 隐私政策页面 -->
  <view class="box">
    <rich-text :nodes=content
               style="font-size: 30rpx;"></rich-text>
  </view>
</template>

<script>
import { GetSysContentByID } from '../api/agreement'
export default {
  data () {
    return {
      content: '',
    }
  },
  methods: {
    getAgreement () {
      var result = {
        action: 'GetSysContentByID',
        ID: 3,
      }
      GetSysContentByID(result).then((res) => {
        this.content = res.data.Data.Contents
      })
    },
  },
  onLoad () {
    this.getAgreement()
  },
}
</script>

<style>
.box {
  padding: 30rpx;
  background-color: #fff;
}
</style>
