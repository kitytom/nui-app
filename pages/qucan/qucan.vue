<template>
      <view class="cart">
          <view class="content">
              <view class="list" v-for="item in list" :key='item.id'>
                  <view class="left">
                      <checkbox-group @change="checkboxChange($event,item.id)">
                          <checkbox :value="item.id" :checked="item.isChecked" />
                      </checkbox-group>
                      <image :src="item.img" class="img"></image>
                  </view>
                  <view class="center">
                      <view class="name">
                          {{item.name}}
                      </view>
                      <view class="size">
                          尺寸：{{item.size}}
                      </view>
                      <view class="count">
                          数量：x{{item.count}}
                      </view>
                  </view>
                  <view class="right">
                      <view class="price">
                          单价￥{{item.price}}元
                      </view>
                      <view class="update-count">
                          <view class="reduce" @tap="editNum(item.id,-1)">
                              -
                          </view>
                          <view class="cart-count">
                              {{item.count}}
                          </view>
                          <view class="add" @tap="editNum(item.id,1)">
                              +
                          </view>
                      </view>
                  </view>
              </view>
          </view>
  
          <!-- 底部导航栏 -->
          <view class="tabbar">
              <view class="all">
                  <checkbox-group @change="checkboxChangeAll">
                      <checkbox :checked="isAllChecked" />全选
                  </checkbox-group>
              </view>
              <view class="totalPrice">
                  总价:￥{{totalPrice}}元
              </view>
              <view 
              class="submitOrder" 
              @tap="submitOrder" >
                  付款
              </view>
          </view>
      </view>
  </template>
  <script>
      export default {
          data() {
              return {
                  list: [], //列表数据
                  isAllChecked: false, //是否全选
                  totalPrice: 0, //总价
              }
          },
          methods: { 
              setCart() { //计算总价
                  let totalPrice = 0
                  this.list.forEach(v => {
                      if (v.isChecked) {
                          totalPrice += v.count * v.price
                      }
                  })
                  this.totalPrice = totalPrice
              },
  
              editNum(id, type) { //编辑数量
                  const index = this.list.findIndex(v => v.id == id)
                  if (this.list[index].count == 1 && type == -1) {
                      uni.showToast({
                          title: '至少购买一件商品',
                          icon: 'none'
                      })
                  } else {
                      this.list[index].count += type
                  }
                  this.setCart()
              },
  
              // 全选
              checkboxChangeAll(e) {
                  this.isAllChecked = !this.isAllChecked
                  this.list.forEach(v => v.isChecked = this.isAllChecked)
                  this.setCart()
              },
  
              // 选择每一项
              checkboxChange: function(e, id) {
                  var temp = []
  
                  // 找到被修改的商品对象
                  let index = this.list.findIndex(v => v.id === id)
                  // 选中状态取反
                  this.list[index].isChecked = !this.list[index].isChecked
  
                  temp = this.list.every(v => v.isChecked)
                  if (temp) {
                      this.isAllChecked = true
                  } else {
                      this.isAllChecked = false
                  }
                  this.setCart()
              },
  
              submitOrder() { // 提交购物车订单
                  // 判断是否选择购物车商品
                  var bol = this.list.every(el => el.isChecked == false)
                  if (bol) {
                      uni.showToast({
                          title: "这些你都不喜欢吗，你是不是只喜欢喝水，你倒是选一个啊商品啊",
                          icon: "none",
                          duration: 2000
                      })
                  } else {
                      uni.showToast({
                          title: "你肯定没有钱,还是算了吧",
                          icon: "none",
                          duration: 2000
                      })
                  }
              }
          },
          onShow() {
              // 模拟从后台拿到的数据
              var list = [
                  {
                      id: '1',
                      name: '可乐鸡翅',
                      price: 12,
                      count:1,
                      size: '大份',
                      img: '../../static/homswiper/3.png'
                  },{
                      id: '2',
                      name: '火锅',
                      price: 30,
                      count: 1,
                      size: '大份',
                      img: '../../static/homswiper/3.png'
                  }
              ]
              // list数组中为每一项添加双向绑定的属性---这个属性要在页面显示(onShow)添加
              list.forEach(el => el.isChecked = false);
              this.list = list;
          },
      }
  </script>
  <style lang="scss" scoped>
      page {
          background: #f1e8e7;
      }
      .content {
          width: 670rpx;
          margin: 0 auto 180rpx;
      }
  
      // 居中显示
      @mixin textCenter {
          display: flex;
          align-items: center;
          justify-content: center;
      }
  
      .list {
          width: 672rpx;
          height: 208rpx;
          background: #f9f9f9;
          box-shadow: 0 8rpx 16rpx 0 rgba(83, 66, 49, 0.08);
          border-radius: 24rpx;
          margin-top: 32rpx;
          display: flex;
          justify-content: space-around;
          align-items: center;
  
          .left {
              display: flex;
  
              .img {
                  width: 136rpx;
                  height: 136rpx;
                  margin-left: 10rpx;
                  border-radius: 8%;
              }
          }
  
          .center {
              width: 170rpx;
  
              .name {
                  font-size: 26rpx;
                  color: #3E3E3E;
                  white-space: nowrap;
                  text-overflow: ellipsis;
                  overflow: hidden;
              }
              .size,
              .count {
                  font-size: 22rpx;
                  color: #8D8D8D;
              }
          }
  
          .right {
              .price {
                  margin-top: 40rpx;
                  font-size: 26rpx;
                  margin-left: 40rpx;
              }
  
              // 加减数量
              .update-count {
                  margin-top: 40rpx;
                  display: flex;
  
                  .reduce,
                  .add {
                      width: 40rpx;
                      height: 40rpx;
                      background: #F1ECE7;
                      border-radius: 21.6rpx;
                      color: #979797;
                      @include textCenter;
                      font-size: 50rpx;
                  }
  
                  .cart-count {
                      width: 72rpx;
                      height: 40rpx;
                      line-height: 40rpx;
                      background: #F1ECE7;
                      border-radius: 21.6rpx;
                      margin-left: 18rpx;
                      margin-right: 18rpx;
                      text-align: center;
                  }
              }
          }
      }
  
      // 底部导航
      .tabbar {
          width: 100%;
          height: 176rpx;
          background-color: #f3f3f3;
          position: fixed;
          bottom: 0rpx;
          display: flex;
          align-items: center;
          justify-content: space-around;
          border-radius: 8% 8%;
  
          .all {
              font-size: 32rpx;
              color: #3E3E3E;
              letter-spacing: 2.29rpx;
              display: flex;
          }
  
          .totalPrice {
              font-size: 32rpx;
              color: #3E3E3E;
              letter-spacing: 2.29rpx;
              color: red;
          }
  
          .submitOrder {
              width: 208rpx;
              height: 80rpx;
              background: #354E44;
              border-radius: 14rpx;
              border-radius: 14rpx;
              font-size: 36rpx;
              color: #FFFFFF;
              letter-spacing: 2.57rpx;
              display: flex;
              align-items: center;
              justify-content: center;
          }
      }
  </style>