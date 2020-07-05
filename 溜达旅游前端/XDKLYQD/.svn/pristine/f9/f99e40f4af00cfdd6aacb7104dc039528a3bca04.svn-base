<template>
  <!-- 权利声明页面 -->
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
        ID: 1,
      }
      GetSysContentByID(result).then((res) => {
        console.log(res)
        this.content = res.data.Data.Contents
      })
    },
  },
  onLoad () {
    // 获取权利声明页面
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
