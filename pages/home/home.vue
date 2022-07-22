<template>
  <view>
    <view class="com_header">
               <view class="com_header_left">
                   <uni-icons type="left" size="26"></uni-icons>
               </view>
               <view class="com_header_center">李先生</view>
               <view class="com_header_right"></view>
           </view>
    <!-- 页面内容 -->
    <view>
      <!-- 轮播 -->
     <!-- <view style="margin-bottom: 5rpx;">
        <swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval"
          :duration="duration" circular="true">
          <swiper-item>
            <view @click="getBanner()"><img src="../../static/home/lunbo.jpg" alt="" style="width: 100%; height: 100%;">
            </view>
          </swiper-item>
          <swiper-item>
            <view @click="getBanner()">
              <img src="../../static/home/lunbo.jpg" alt="" style="width: 100%; height: 100%;">
            </view>
          </swiper-item>
          <swiper-item>
            <view @click="getBanner()">
              <img src="../../static/home/lunbo.jpg" alt="" style="width: 100%; height: 100%;">
            </view>
          </swiper-item>
        </swiper>
      </view> -->
    </view>
    <view style="display: flex; justify-content: space-around;">
      <view style="display: flex; flex-direction: column;align-items: center; width: 100rpx;">
        <img src="../../static/logo.png" alt="" style="width: 100rpx;">
        <text>shop</text>
      </view>
      <view style="display: flex; flex-direction: column;align-items: center; width: 100rpx;">
        <img src="../../static/logo.png" alt="" style="width: 100rpx;">
        <text>news</text>
      </view>
      <view style="display: flex; flex-direction: column;align-items: center; height: 100rpx;">
        <img src="../../static/logo.png" alt="" style="width: 100rpx;">
        <text>home</text>
      </view>
    </view>
  </view>
</template>
<script>
  export default {
    data() {
      return {
        // 状态栏高度
        statusBarHeight: 0,
        // 导航栏高度
        navBarHeight: 82 + 11,
        indicatorDots: true,
        autoplay: true,
        interval: 2000,
        duration: 500
      };
    },
    props: {

    },
    methods: {
      getBanner() {
        uni.navigateTo({
          url: '../banner/banner',
          success() {
            console.log("跳转成功");
          },
          fail() {
            console.log("跳转失败");
          }
        })
      }
    },
    //第一次加载时调用
    created() {
      //获取手机状态栏高度
      this.statusBarHeight = uni.getSystemInfoSync()['statusBarHeight'];
    },
  }

</script>
<style lang="scss">
 .com_header{
     position: fixed;
     z-index: 1001;
     top:0;
     left:0;
     width: 100%;
     height: 88rpx;
     width: 100%;
     display: flex;
     padding-top:var(--status-bar-height);
     line-height: 88rpx;
     background: #fff;
     .com_header_left{
         flex:25%;
         height:100%;
         padding-left:32rpx;
     }
     .com_header_center{
         flex:40%;
         height:100%;
         text-align: center;
         color: #111111;
         font-weight: bold;
         font-size: 36rpx;
     }
     .com_header_right{
         flex:25%;
         height:100%;
         padding-right:32rpx;
         text-align: right;
         color:#222;
         font-size:32rpx;
     }
 }
</style>