<template>
  <view style="height: 100%;">
    <view class="com_header" :style="{paddingTop: statusBar + 'px'}">
              
               <view class="com_header_center">
				   <input type="text" style="border: 1px solid black; border-radius: 10px; "
				     placeholder="点击搜索" @click="setDisplay" value="">
			   </view>
               
           </view>
    <!-- 页面内容 -->
    <view class="content1" :style="{paddingTop: customBar + 'px'}">
		<!-- <scroll-view :scroll-top="scrollTop" scroll-y="true" class="scroll-Y" @scrolltoupper="upper"
					 @scrolltolower="lower" @scroll="scroll" style="height: 100%;"> -->
						<view style="margin-bottom: 5rpx;" >
							<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval"
							        :duration="duration" circular="true">
							    <swiper-item v-for="(item,index) in banners" :key="item.typeTitle">							       
									<image :src='item.pic' @click="getBanner"></image>						       
							     </swiper-item>
							     
							</swiper>
						</view>
						
						<list class='popList'>
						  <view v-for="(item, index) in dataList" :key="item.id">
							  <image :src='item.img' ></image>
							  <span>{{item.name}}</span>
						  </view>
						</list>
						<view class='morePop'>
							<span>推荐歌单</span>
							<span class='moreMusic' @click='more'>更多 ></span>
						</view>
						<list class='musList'>
						  <view v-for="(item, index) in playlists" :key="item.id" @click="getPop(item.id)">
							  <image :src='item.coverImgUrl'></image>
							  <span>{{item.name}}</span>
						  </view>
						</list>
						<view class='morePop' style='margin-top: 50rpx;'>
							<span>歌曲列表</span>
							<span class='moreMusic' @click='more'>更多 ></span>
						</view>
						<list class="musicList" v-for="(item,index) in musicList" :key="item.id">
							<image :src="item.album.blurPicUrl"></image>
							<view>
								<span>{{item.name}}</span>
								<span>{{item.album.subType}}</span>
							</view>
							<span>播放</span>
						</list>
						<view class="bookshelf">
						      <view class="title">
						        <span>排行</span>
						        <span class='moreMusic' @click='more'>更多 ></span>
						      </view>
						      <scroll-view scroll-x="true" class="bookshelf-content">
						        <block v-for="(item, index) in hotlist" :key="index">
						          <view class="item" @tap="goDetail(item.id)">
						            <view class="img">
						              <image :src='item.coverImgUrl'></image>
						            </view>
						            <span class="item-title text-over-1">{{item.name}}</span>
						          </view>
						        </block>
						      </scroll-view>
						    </view>
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
		banners:[],
		dataList: [{id: "1", name: '推荐',img:'../../static/hot_fill.png'}, {id: "2", name: '列表',img:'../../static/列表模式.png'}, {id: "3", name: '排行',img:'../../static/排行.png'},{id: "4", name: '电台',img:'../../static/电台.png'}],
		playlists: [],
		hotlist:[],
		musicList:[
			{id:'1',name:'千本樱',sing:'初音未来',img:'../../static/logo.png'},
			{id:'2',name:'霜雪千年',sing:'洛天依',img:'../../static/logo.png'},
			{id:'3',name:'badApple',sing:'zun',img:'../../static/logo.png'},
			{id:'4',name:'千本樱',sing:'初音未来',img:'../../static/logo.png'},
			],
		searchHistory:[]
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
	 setDisplay() {
	 	uni.navigateTo({
	 		url:'../searchs/searchs',
			success() {
				console.log('search');
			}
	 	})
	 },
	 getvalue(e) {
		 console.log(e.detail.value);
		 uni.setStorage({
			 key:'sHistory',
			 data:e.detail.value,
			 success() {
			 	console.log('success');
			 }
		 })
		 
	 }
    },
    created() {
		uni.request({
			url:`${this.$baseUrl}/top/playlist?limit=10&order=hot`,
			method:"GET",
			success: (res) => {
				console.log(res.data);
				this.playlists = res.data.playlists
			},
			fail: (err) => {
				console.log(err);
			}
		}),
		uni.request({
			url:`${this.$baseUrl}/playlist/catlist`,
			method:"GET",
			success: (res) => {
				console.log(res);
			},
			fail: (err) => {
				console.log(err);
			}
		})
		uni.request({
			url:`${this.$baseUrl}/toplist`,
			method:"GET",
			success: (res) => {
				console.log(res);
				this.hotlist = res.data.list
			},
			fail: (err) => {
				console.log(err);
			}
		})
		uni.request({
			url:`${this.$baseUrl}/top/song?type=8`,
			method:"GET",
			success: (res) => {
				console.log(res,1111111111111111111111);
				this.musicList = res.data.data.slice(0,10)
			},
			fail: (err) => {
				console.log(err);
			}
		})
		uni.request({
			url:`${this.$baseUrl}/banner?type=2`,
			method:"GET",
			success: (res) => {
				console.log(res);
				this.banners = res.data.banners
			},
			fail: (err) => {
				console.log(err);
			}
		})
		console.log(this.$baseUrl);
		
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
	onShow() {
		uni.request({
			url:`${this.$baseUrl}/login/status`,
			method:"GET",
			success: (res) => {
				if(res.data) {
					if(res.data.code == '-462') {
						uni.navigateTo({
							url:'../login/login',
							success() {
								console.log('成功');
							}
						})
					}
				}
			},
			fail: (err) => {
				console.log(err);
			}
		})
		
	}
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
.content1 {
	height: 100%;
	image {
		display: block;
		height: 100%;
		width: 100%;
	}
	.popList {
		display: flex;
		margin: 20rpx 0 10rpx 0;
		view {
			text-align: center;	
			width: 100%;
			height: 150rpx;
			line-height: 70rpx;
		}
		image {
			border-radius: 50%;
			margin:0 auto;
			width: 40%;
			height: 70%;
			display: block;
		}
	}
	.morePop {
		margin: 80rpx 0 30rpx 0;
		display: flex;
		justify-content: space-between;
		font-size: 20px;
		padding: 0 30rpx 0 20rpx;
		
	}
	.bookshelf {
	      margin-top: 50rpx;
	      .bookshelf-content {
	        white-space: nowrap; // 滚动必须加的属性
	        width: 100%;
	        height: 300rpx;
	        padding: 20rpx;
	        margin: 0 auto;
	        .item {
	          width: 24%;
	          margin-right: 20rpx;
	          display: inline-block;
	          vertical-align: top;
	          .img {
	            display: inline-block;
	            image {
	              width: 170rpx;
	              height: 220rpx;
	              border-radius: 6rpx;
	            }
	          }
	          .item-title {
	            display: block;
				 white-space: normal;// 让字体换行
	            width: 90%;
	            font-size: 30rpx;
	            line-height: 40rpx;
	          }
	        }
	      }
		  .title {
			  display: flex;
			  justify-content: space-between;
			  font-size: 20px;
			  padding: 0 30rpx 0 20rpx;
		  }
	    }
	.musList {
		display: flex;
		flex-flow: wrap;
		view {
			padding:0 0 180rpx 20rpx;
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
			font-size: 14px;
		}
		span {
			
			flex: 15%;
		}
	}
	.ranking {
		display: flex;
		// width: 1350rpx;
		overflow: hidden;
		// flex-flow: wrap;
		view {
			padding:0 0 50rpx 20rpx;
			width: 200rpx !important;
			height: 200rpx;
			text-align: center;
		}
	}
}
</style>