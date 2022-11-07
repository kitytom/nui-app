<template>
	<view class="content">
		<swiper circular="true"
    autoplay="true"
    interval="2000"
    >
      <swiper-item class="swiperhome">
        <image src="../../static/index/index1.jpg"></image>
        <view class="navgater" @click="getuser">
         进入小程
        </view>
      </swiper-item>
      <swiper-item class="swiperhome">
         <image src="../../static/index/index2.jpg"></image>
         <view class="navgater"  @click="getuser">
         进入小程
         </view>
      </swiper-item>
      <swiper-item class="swiperhome">
         <image src="../../static/index/index4.jpg"></image>
         <view class="navgater" @click="getuser">
         进入小程
         </view>
      </swiper-item>
    </swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
        avatarUrl:'',
        nickName:'',
        userInfo:''
			}
		},
		onLoad() {

		},
		methods: {
   getuser(){
        let that = this
        uni.getUserProfile({
          desc:'用户登录用户',
          success:function(res){
            that.nickName = res.userInfo.nickName
            that.avatarUrl = res.userInfo.avatarUrl
            console.log( that.avatarUrl)
            that.getlocde(that.nickName, that.avatarUrl)
            uni.switchTab({
              url:'/pages/home/home'
            })
          }
        })
    },
       getlocde(step1,step2){
         wx.setStorage({
           key:'nickName',
           data: step1
         })
         wx.setStorage({
           key:'avatarUrl',
           data: step2
         })
       }
    }
	}
</script>

<style>
  page{
    height:100%;
   }
  .content{
    width: 100%;
    height: 100%; 
   }
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
swiper{
  width: 100%;
  height: 1250rpx;
}
  
swiper-item image{
  width: 100%;
  height: 100%;
}
.swiperhome{
  position: relative;
}
.navgater{
  position: absolute;
  bottom:100rpx;
  left: 100rpx;
  color: red;
}
</style>
