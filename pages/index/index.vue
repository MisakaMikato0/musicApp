<template>
  <view style="height: 100%;">
    <view class="com_header" :style="{paddingTop: statusBar + 'px'}">
              
               <view class="com_header_center">
				   <input type="text" style="border: 1px solid black; border-radius: 10px; "
				     placeholder="请输入歌曲内容">
			   </view>
               
           </view>
    <!-- 页面内容 -->
    <view class="content" :style="{paddingTop: customBar + 'px'}">
		<!-- <scroll-view :scroll-top="scrollTop" scroll-y="true" class="scroll-Y" @scrolltoupper="upper"
					 @scrolltolower="lower" @scroll="scroll" style="height: 100%;"> -->
						<view style="margin-bottom: 5rpx;" >
							<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval"
							        :duration="duration" circular="true">
							    <swiper-item>							       
									<image src="../../static/home/lunbo.jpg" @click="getBanner"></image>						       
							     </swiper-item>
							     <swiper-item>							       
							         <image src="../../static/home/lunbo.jpg" alt="" @click="getBanner"></image>							       
							     </swiper-item>
							     <swiper-item>							       
							         <image src="../../static/home/lunbo.jpg" alt="" @click="getBanner"></image>							
							     </swiper-item>
							</swiper>
						</view>
						
						<list class='popList'>
						  <view v-for="(item, index) in dataList" :key="item.id">
							  <image src='../../static/logo.png'></image>
							  <span>{{item.name}}</span>
						  </view>
						</list>
						<view class='morePop'>
							<span>推荐歌单</span>
							<span class='moreMusic' @click='more'>更多 ></span>
						</view>
						<list class='musList'>
						  <view v-for="(item, index) in musList" :key="item.id" @click="getPop(item.id)">
							  <image src='../../static/logo.png'></image>
							  <span>{{item.name}}</span>
						  </view>
						</list>
						<view class='morePop' style='margin-top: 50rpx;'>
							<span>歌曲列表</span>
							<span class='moreMusic' @click='more'>更多 ></span>
						</view>
						<list class="musicList" v-for="(item,index) in musicList" :key="item.id">
							<image :src="item.img"></image>
							<view>
								<span>{{item.name}}</span>
								<span>{{item.sing}}</span>
							</view>
							<span>播放</span>
						</list>
						<view class='morePop' style='margin-top: 50rpx;'>
							<span>排行榜</span>
							<span class='moreMusic' @click='more'>更多 ></span>
						</view>
						<scroll-view scroll-x='true'>
							<view class='ranking'>
							  <view v-for="(item, index) in musList" :key="item.id">
								  <image src='../../static/logo.png'></image>
								  <span>{{item.name}}</span>
							  </view>
							</view>
						</scroll-view>
		<!-- </scroll-view>  -->
			  
    </view>
   
  </view>
</template>
<script>
  export default {
    data() {
      return {
        // 状态栏高度
        statusBar: 0,
        // 导航栏高度
        customBar: 0,
        indicatorDots: true,
        autoplay: true,
        interval: 2000,
        duration: 500,
		dataList: [{id: "1", name: '推荐'}, {id: "2", name: '列表'}, {id: "3", name: '排行'},{id: "4", name: '电台'}],
		musList: [
			{id: "1", name: '古风'},
			{id: "2", name: '现代'},
			{id: "3", name: '二次元ACG'},
			{id: "4", name: '东方Project'},
			{id: "5", name: '复古'},
			{id: "6", name: '晚安'},			
			],
		musicList:[
			{id:'1',name:'千本樱',sing:'初音未来',img:'../../static/logo.png'},
			{id:'2',name:'霜雪千年',sing:'洛天依',img:'../../static/logo.png'},
			{id:'3',name:'badApple',sing:'zun',img:'../../static/logo.png'},
			{id:'4',name:'千本樱',sing:'初音未来',img:'../../static/logo.png'},
			]
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
	  more() {
		  uni.navigateTo({
		  	url:`../more/more`,
			success() {
				console.log('跳转成功');
			},
			fail() {
				console.log('跳转失败');
			}
		  })
	  },
	 getPop(id) {
	   uni.navigateTo({
	     url: `../show/show?type=${id}`,
	     success() {
	       console.log("跳转成功");
	     },
	     fail() {
	       console.log("跳转失败");
	     }
	   })
	 },
    },
    created() {
	  uni.getSystemInfo({
	      success: (e) => {
	        let statusBar = 0
	        let customBar = 0
	        
	        
	        // #ifdef MP
	        statusBar = e.statusBarHeight
	        customBar = e.statusBarHeight + 45
	        if (e.platform === 'android') {
	          this.$store.commit('SET_SYSTEM_IOSANDROID', false)
	          customBar = e.statusBarHeight + 50
	        }
	        // #endif
	        
	        
	        // #ifdef MP-WEIXIN
	        statusBar = e.statusBarHeight
	        // @ts-ignore
	        const custom = wx.getMenuButtonBoundingClientRect()
	        customBar = custom.bottom + custom.top - e.statusBarHeight
	        // #endif
	  
	  
	        // #ifdef MP-ALIPAY
	        statusBar = e.statusBarHeight
	        customBar = e.statusBarHeight + e.titleBarHeight
	        // #endif
	  
	  
	        // #ifdef APP-PLUS
	        console.log('app-plus', e)
	        statusBar = e.statusBarHeight
	        customBar = e.statusBarHeight + 45
	        // #endif
	  
	  
	        // #ifdef H5
	        statusBar = 0
	        customBar = e.statusBarHeight + 45
	        // #endif
	  
	        this.statusBar = statusBar
	        this.customBar =  customBar
	      }
	  })
    },
  }

</script>
<style lang="scss">
page {
	height: 100%;
}
.com_header{
    position: fixed;
    z-index: 1001;
    top:0;
    left:0;
    width: 100%;
    height: 88rpx;
    width: 100%;
    display: flex;
	justify-content: flex-start;
    padding-top:var(--status-bar-height);
    line-height: 88rpx;
    background: #fff;
  
    .com_header_center{
		margin-left: 150rpx;
        height:100%;
        text-align: center;
        color: #111111;
        font-weight: bold;
        font-size: 30rpx;
		display: flex;
		align-items: center;
    }
   
}
.content {
	height: 100%;
	image {
		display: block;
		height: 100%;
		width: 100%;
	}
	.popList {
		display: flex;
		margin: 20rpx 0;
		view {
			text-align: center;	
			width: 100%;
			height: 150rpx;
			line-height: 70rpx;
		}
		image {
			border-radius: 50%;
			margin:0 auto;
			width: 50%;
			height: 80%;
			display: block;
		}
	}
	.morePop {
		margin: 100rpx 0 30rpx 0;
		display: flex;
		justify-content: space-between;
		font-size: 20px;
		padding: 0 30rpx 0 20rpx;
		
	}
	.musList {
		display: flex;
		flex-flow: wrap;
		view {
			padding:0 0 50rpx 20rpx;
			width: 225rpx;
			height: 200rpx;
			text-align: center;
		}
	}
	.musicList {
		padding: 0 0 10rpx 20rpx;
		display: flex;
		justify-content: space-between;
		align-items: center;
		image {
			flex: 15%;
			width: 100rpx;
			height: 100rpx;
		}
		view{
			flex: 70%;
			padding-left: 30rpx;
			display: flex;
			flex-direction: column;
		}
		span {
			
			flex: 15%;
		}
	}
	.ranking {
		display: flex;
		width: 1350rpx;
		overflow: hidden;
		// flex-flow: wrap;
		view {
			padding:0 0 50rpx 20rpx;
			width: 200rpx;
			height: 200rpx;
			text-align: center;
		}
	}
}
</style>