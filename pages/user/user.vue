<template>
  <view style="height: 100%;">
		<view class="userTop">
			<image src="../../static/logo.png"></image>
			<text>{{userInfo.name}}</text>
		</view>
		<view class="content">
			<view>
				<image src="../../static/tapbar/user.png" mode=""></image>
				<span>我的信息</span>
			</view>
			<view>
				<image src="../../static/vip.png" mode=""></image>
				<span>我的VIP</span>
			</view>
			<view>
				<image src="../../static/好友.png" mode=""></image>
				<span>我的好友</span>
			</view>
			<view>
				<image src="../../static/歌单 (1).png" mode=""></image>
				<span>我的歌单</span>
			</view>
			<view>
				<image src="../../static/进入.png" mode=""></image>
				<span @click='bcakUser'>退出登录</span>
			</view>
		</view>
   
  </view>
</template>
<script>
  export default {
    data() {
      return {
		userInfo:{
			name:'Misaka'
		}
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
      },
	  bcakUser() {
		  uni.request({
		  	url:`${this.$baseUrl}/logout`,
			method:'GET',
			success(res) {
				console.log(res);
			}
		  })
	  }
    },
    //第一次加载时调用
    created() {
    
  },
	onShow() {
		uni.request({
			url:`${this.$baseUrl}/user/playlist?uid=32953014`,
			method:"GET",
			success(res) {
				console.log(res);
			}
		})
	}
	
}

</script>
<style lang="scss">
  .userTop {
	  background-color: #bfbfbf;
	  font-size: 20px;
	  padding:30rpx 150rpx 30rpx 30rpx;
	  margin-bottom: 20rpx;
	  display: flex;
	  justify-content: space-around;
	  align-items: center;
	  image {
		  border-radius: 50%;
		  width: 170rpx;
		  height: 170rpx;
	  }
  }
  .content {
	  view {
		  background-color: #bfbfbf;
		  display: flex;
		  justify-content: space-between;
		  padding:0 400rpx 0 100rpx;
		  height: 100rpx;
		  line-height: 100rpx;
		  margin-bottom: 20rpx;
		  &:active {
			  background-color: #f5f5f5;
		  }
	  }
	  image {
		  margin: auto 0;
		  width: 70rpx;
		  height: 70rpx;
	  }
  }
</style>