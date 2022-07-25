<template>
	<view>
		<view class="searchTop">			
			<input type="text" style="border: 1px solid black; border-radius: 10px; "
				   placeholder="请输入歌曲名字" @confirm="onSearch">
			<span @click='goBack'>取消</span>
		</view>
		<view >
			<view class="hotTitle">
				<span>热门搜索</span>
				<!-- <image src="../../static/删除.png" mode="" @click="hisDel"></image> -->
			</view>
			<view class="hotList"></view>
		</view>
		<view>
			<view class="hisSearch">
				<span>历史搜索</span>
				<image src="../../static/删除.png" mode="" @click="hisDel"></image>
			</view>	
			<view class="historys">
				<view v-for="(item,index) in searchRecord" :key="item.id">{{item.value}}</view>
				<view v-if="searchRecord.length == 0" style="text-align:center;width: 100%;">没有搜索历史</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				inputVal:'',
				searchRecord:[],
				hotSearch: [{
					value:'稻香',
					id:0
				},
				{
					value:'求佛',
					id:1
				},
				{
					value:'badApple',
					id:2
				},
				{
					value:'千本樱',
					id:3
				},
				{
					value:'墨染之樱',
					id:4
				}]
			}
		},
		methods: {
			goBack() {
				
				uni.navigateBack()
			},
			getHistorySearch() {
				
					this.searchRecord = uni.getStorageSync("searchRecord") || []
				
			},
			hisDel: function() {
			  uni.clearStorageSync('searchRecord')
			  this.searchRecord = []
			},
			onSearch(e) {
				console.log(e.detail);
				let inputVal = e.detail.value
				let searchRecord = this.searchRecord
				if (inputVal == '') {
					return false
				} else {
					if (searchRecord.length < 8) {
						searchRecord.unshift({
							value:inputVal,
							id:searchRecord.length
						})
					} else {
						 searchRecord.pop() //删掉时间最早的一条
						      searchRecord.unshift({
						        value: inputVal,
						        id: searchRecord.length,
						        
						      })
					}
				}
				uni.setStorageSync('searchRecord', searchRecord)
			}
		},
		onLoad:function() {
			this.getHistorySearch()
			console.log(1111111111);
		}
	}
	
</script>

<style lang="scss">
.searchTop {
	display: flex;
	justify-content: space-around;
	// padding: 0 40rpx;
	input {
		width: 450rpx;
		text-align: center;
	}
}
.hisSearch {
	display: flex;
	justify-content: space-between;
	padding: 0 40rpx;
	align-items: center;
	image {
		width: 50rpx;
		height: 50rpx;
	}
	
}
.historys {
		display: flex;
		justify-content: flex-start;
		flex-wrap: wrap;
		view {
			padding: 10rpx 20rpx;
		}
	}
.hotTitle {
	display: flex;
	justify-content: space-between;
	padding: 10rpx 40rpx;
	align-items: center;
}
</style>
