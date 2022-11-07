<template>
  <view>
    <view class="dindanbox">
      <view class="dindanbox-left"
       :class="{'active':newshow}"
      v-on:click="newnum">
        当前订单
      </view>
      <view class="dindanbox-right" 
      :class="{'active':oldershow}"
      v-on:click="olderdindan">
        历史订单
      </view>
    </view>
    <!--  -->
     <view class="itemnumber" v-if="newshow">
      <image src="../../static/homswiper/2.png" alt="">
        <view class="text">
        <text> 订单编号：120365</text>
        <text>金额：￥35.0</text>
        </view>
     </view>
     <view class="itemnumber" v-if="newshow">
      <image src="../../static/homswiper/2.png" alt="">
        <view class="text">
        <text> 订单编号：120365</text>
        <text>金额：￥35.0</text>
        </view>
     </view>
     <!--  -->

     <view class="itemnumber" v-if="oldershow">
      <image src="../../static/homswiper/2.png" alt="">
        <view class="text">
        <text> 订单编号：120365</text>
        <text>金额：￥35.0</text>
        </view>
  </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        newshow:true,
        oldershow:false
      }
    },
    methods: {
      newnum(){
        console.log('lll')
        this.oldershow=false
        this.newshow=true
      },
      olderdindan(){
        console.log('pp')
        this.oldershow=true
        this.newshow=false
      }
    }
  }
</script>

<style scoped>
  .active{
    color: #db6eff;
  }
.dindanbox{
  height: 100rpx;
  display: flex;
  line-height: 100rpx;
  text-align: center;
  background-color: antiquewhite;
}
.dindanbox-left,.dindanbox-right{
  width: 400rpx;
}
.itemnumber{
  display: flex;
  margin-bottom: 20rpx;
}
.itemnumber image{
  width: 200rpx;
  height: 200rpx;
  margin-left: 20rpx;
}
.itemnumber text{
  margin: 20rpx;
  display: block;
}
</style>
