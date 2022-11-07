<template>
  <view  class="homebox">
 <swiper circular="true" autoplay="true"interval="2000" class="home-swiper">
   <swiper-item>
     <image src="../../static/homswiper/1.png"></image>
   </swiper-item>
   <swiper-item>
      <image src="../../static/homswiper/2.png"></image>
   </swiper-item>
   <swiper-item>
      <image src="../../static/homswiper/3.png"></image>
   </swiper-item>
 </swiper>
 <!--  -->
    <view class="content">
      <view class="content-left">
        <navigator open-type="switchTab" url="../goods/goods">
        <image src="../../static/homswiper/index1.png" alt=""></navigator>
      </view>
      <view class="content-right">
       
        <image src="../../static/homswiper/index2.png" alt="">
      </view>
    </view>
    <!--  -->
    <view class="bottombox">
      <view class="bottombox-left">
        成为我们的会员吧
      </view>
      <view class="bottombox-right">
       <navigator open-type="switchTab" url="../my/my"> 去注册</navigator>
      </view>
    </view>
    <!--  -->
    <view class="bottombox">
      <view class="bottombox-left">
        店内就餐请扫桌子上二维码
      </view>
      <view class="bottombox-right">
      <image src="../../static/shao.png" @click="shaoma"></image>
      </view>
    </view>
    <!--  -->
    <view class="goodstitle">
      众多美食等你来
    </view>
    <view class="goodsitem">
       <navigator open-type="switchTab" url="../goods/goods">
         <image src="../../static/homswiper/img1.jpg"></image>
       </navigator>
        <navigator open-type="switchTab" url="../goods/goods">
       <image src="../../static/homswiper/img2.jpg"></image>
         </navigator>
          <navigator open-type="switchTab" url="../goods/goods">
       <image src="../../static/homswiper/img3.jpg"></image>
           </navigator>
            <navigator open-type="switchTab" url="../goods/goods">
       <image src="../../static/homswiper/img4.jpg"></image>
           </navigator>
    </view>
    </view>
  
</template>

<script>
  export default {
    data() {
      return {
        // 接受扫码获取的参数
        snumber:''
      }
    },
    methods: {
      // 扫码获取桌号
      shaoma(){
        var that = this
        wx.scanCode({
          onlyFromCamera:true,
          success(res){
            // console.log(JSON.stringify(res))
            that.snumber=res.result
            // console.log(that.snumber)
            wx.setStorage({
              key:'number',
              data:res.result
            })
            // 扫码成功后跳转到商品页
            uni.switchTab({
              url:'/pages/goods/goods'
            })
          }
        })
      }
    }
  }
</script>

<style>
  .homebox{
    background-color: #edf4ff;
  }
  .home-swiper{
    height: 330rpx;
    width: 100%;
  }
.home-swiper image{
  width: 100%;
  color: #ffdeae;
}
.content{
  height: 300rpx;
  margin: 20rpx;
  display: flex;
 background-color: #fff2f4; 
}
 .content-left, .content-right{
   width: 400rpx;
   text-align: center;
}
.content-left image, .content-right image{
   height: 280rpx;
   width: 200rpx;
   margin-top: 10rpx;
}
.bottombox{
  height: 200rpx;
  display: flex;
  line-height: 200rpx;
  margin: 20rpx;
  text-align: center;
  background-color:  #fff2f4;
}
.bottombox-left{
  padding-left: 20rpx;
  font-size: 28rpx;
  color: #ff5500;
}
.bottombox-left,.bottombox-right{
  width: 400rpx;
}
.bottombox-right image{
  margin: 50rpx 0rpx 0rpx 0rpx;
  width: 100rpx;
  height: 100rpx;
}
.goodsitem {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
.goodsitem image{
  width: 330rpx;
  height: 240rpx;
  margin: 10rpx;
}
.goodstitle{
  height: 45rpx;
  margin-left: 40rpx;
}
</style>
