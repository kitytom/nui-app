<template>
  <view>
    <view class="mybox">
      <image src="../../static/homswiper/2.png"></image>
    </view>
    <view class="userbox">
      <image :src="avatarUrl" mode=""></image>
    <!-- <open-data type="userAvatarUrl"></open-data> -->
     <text>昵称--{{nickName}}</text>
     <view class="loginbox">
       <navigator open-type="navigate">去注册</navigator>
     <navigator open-type="navigate">去登录</navigator>
     </view>
     
    </view>
    <!--  -->
    <view class="myitem">
      <view class="dindan">
        我的订单
      </view>
      <view class="dindan">
        我的购物车
      </view>
      <view class="dindan">
        关于我们
      </view>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        nickName:'',
        avatarUrl:'',
        userInfo:''
      }
    },
    created(){
      console.log('00')
     this.nickName = uni.getStorageSync('nickName')
     this.avatarUrl = uni.getStorageSync('avatarUrl')
    },
    methods: {

    }
  }
</script>

<style>
  page{
    width: 100%;
    height: 100%;
    background-color: #ffe5ea;
  }
.mybox image{
  width: 100%;
}
.userbox{
  height: 300rpx;
  width: 714rpx;
  margin: 0rpx 10rpx 0rpx 20rpx;
  background-color: #ffc1dd;
  position:fixed;
  top: 320rpx;
  border-radius: 10rpx 10rpx 0rpx 0rpx;
}
.userbox image{
  width: 100rpx;
  height: 100rpx;
  border-radius: 100%;
  margin: 50rpx;
}
.userbox {
  display: flex;
}
.userbox text{
  margin-top:90rpx ;
}
 .userbox .loginbox{
   margin: 240rpx 0rpx 0rpx 120rpx;
   width: 300rpx;
   display: flex;
 }
 .loginbox navigator{
   width: 100rpx;
   height: 50rpx;
   line-height: 50rpx;
   text-align: center;
   margin-left: 10rpx;
   border-radius: 10rpx;
   display: inline-block;
   background-color: #ffe5ea;
 }
.myitem{
  margin-top: 200rpx;
}
.dindan{
  height: 90rpx;
  line-height: 90rpx;
  padding-left: 50rpx;
  
}
</style>
