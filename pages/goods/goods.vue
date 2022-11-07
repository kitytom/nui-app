<template>
  <view class="goodsbox">
    <!-- 左侧 -->
   <view class="aside-left">
     <!-- 左侧 -->
     <view 
     class="aside-item" 
     v-on:click="activeclick(1)" 
     v-bind:class="{acticecolor:isactive==1?true:''}">
       top5
     </view>
     <view 
     class="aside-item" 
     v-on:click="activeclick(2)"
      v-bind:class="{acticecolor:isactive==2?true:''}"
     >
       牛排/羊排
     </view>
     <view 
     class="aside-item" 
     v-on:click="activeclick(3)"  
     v-bind:class="{acticecolor:isactive==3?true:''}">
       刺身
     </view>
     <view
     class="aside-item" 
     v-on:click="activeclick(4)"  
     v-bind:class="{acticecolor:isactive==4?true:''}">
       汤类
     </view>
     <view
     class="aside-item" 
     v-on:click="activeclick(5)"  
     v-bind:class="{acticecolor:isactive==5?true:''}">
       虾类
     </view>
     <view
     class="aside-item" 
     v-on:click="activeclick(6)"  
     v-bind:class="{acticecolor:isactive==6?true:''}">
       凉拌
     </view>
     <view
     class="aside-item" 
     v-on:click="activeclick(7)"  
     v-bind:class="{acticecolor:isactive==7?true:''}">
       炒饭
     </view>
     <view
     class="aside-item" 
     v-on:click="activeclick(8)"  
     v-bind:class="{acticecolor:isactive==8?true:''}">
       饮品
     </view>
     <view
     class="aside-item" 
     v-on:click="activeclick(1)"  
     v-bind:class="{acticecolor:isactive==1?true:''}">
       {{zhuohao}}
     </view>
   </view>
   <!-- 左侧 -->
   <!-- 右侧盒子 -->
   <view class="aside-right">
     <view class="goods-item" v-if="show==1?true:''">
       <!-- top5 -->
       <view class="item1" @click="addcart">
         <image src="../../static/homswiper/img3.jpg"></image>
         <text> top1</text>
       </view>
       <view class="item1" v-on:click="addcart">
         <image src="../../static/homswiper/img1.jpg"></image>
         <text> top1</text>
       </view>
       <view class="item1">
         <image src="../../static/homswiper/img2.jpg"></image>
         <text> top1</text>
       </view>
     </view>
     <!-- 牛排 -->
     <view class="goods-item" v-if="show==2?true:''">
       <!-- top5 -->
       <view class="item1" @click="addcart" >
         <image src="../../static/homswiper/1.png"></image>
         <text> 西冷牛排</text>
       </view>
       <view class="item1">
         <image src="../../static/homswiper/3.png"></image>
         <text> 羊排</text>
       </view>
       <view class="item1">
         <image src="../../static/homswiper/1.png"></image>
         <text>半分熟</text>
       </view>
     </view>
     <!--刺身 3 -->
     <view class="goods-item" v-if="show==3?true:''">
       <view class="item1">
         <image src="../../static/homswiper/1.png"></image>
         <text>三文鱼</text>
       </view>
       <view class="item1">
         <image src="../../static/homswiper/3.png"></image>
         <text>金枪鱼</text>
       </view>
       <view class="item1">
         <image src="../../static/homswiper/1.png"></image>
         <text>大虾</text>
       </view>
     </view>
     
     
     
     <!--  -->
     <!--  -->
   </view>
   <view class="showgoods" v-if="gooditem">
       <image src="../../static/homswiper/img3.jpg"></image>
     <view class="title">
       <text>top1-￥1200 </text>
     </view>
     <view class="addbtn">
       <text @click="addsql()">加入购物车</text>
      <text @click="quxaio">取消</text>
     </view>
   </view>

  </view>
</template>

<script>
import { vShow } from "vue"
  export default {
    data() {
      return {
      aside:1,
      isactive:1,
      show:1,
      zhuo:false,
      // 点击食品显示加入购物车
      gooditem:false,
      zhuohao:''
      }
    },
    created(){
      console.log(uni.getStorageSync('number') ) 
      this.zhuohao = uni.getStorageSync('number')
    },
    methods: {
      activeclick(num){
        console.log(num)
        this.isactive=num
        this.show=num
      },
      addcart(){
        console.log('ll')
        this.gooditem=true
      },
      quxaio(){
         this.gooditem=false
      },
      addsql(){
        // 发起请求加入都数据库中
      }
    }
  }
</script>
<style>
  .showgoods{
    width: 400rpx;
    height: 380rpx;
    position: fixed;
    top: 200rpx;
    left: 200rpx;
    border-radius: 10rpx;
    background-color: #e9bbff;
  }
  .showgoods image{
    width: 400rpx;
    height: 240rpx;
  }
  page{
    width: 100%;
    height: 100%;
    background-color: #f9f0ff;
  }
  .goodsbox{
    display: flex;
  }
  .aside-left{
    width: 200rpx;
    height: 1100rpx;
    text-align: center;
    padding-top: 10rpx;
    background-color: #ffd9e5;
  }
   .aside-left .aside-item{
      width: 190rpx;
     height: 70rpx;
     line-height: 70rpx;
     background-color:#ffffff;
     margin-bottom: 10rpx;
   }
  .acticecolor{
    color: #ff5ab2;
    border-left: 10rpx solid #ff5ab2;
  }
  .goods-item{
    display: flex;
    flex-wrap: wrap;
  }
  .item1{
        display: block;
     }
  .goods-item .item1 image{
    display: block;
    margin: 20rpx 15rpx 10rpx 15rpx;
    width: 230rpx;
    height: 100rpx;
  }
    .goods-item .item1 text{
      display: block;
       text-align: center;
    }
    .title{
      height: 65rpx;
      margin-left: 20rpx;
    }
    .addbtn text{
      display: inline-block;
      width: 150rpx;
      height: 60rpx;
      line-height: 60rpx;
      text-align: center;
      border-radius:10rpx ;
      margin-left: 20rpx;
      background-color: #ff5ab2;
    }
</style>