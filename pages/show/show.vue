<template>
	<view class="">
		<view v-if="Tj == '1'">
			<span>111111111111</span>
		</view>
		<view v-if="Tj == '2'">
			<span>222222222222</span>
		</view>
		<view v-if="Tj == '3'">
			<span>33333333333</span>
		</view>
		<view v-if="Tj == '4'">
			<span>44444444444444</span>
		</view>
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				Tj:null
			}
		},
		methods: {
			
		},
		onLoad(option){
			// console.log(this);
			// console.log(Object.keys(option)[0]);
			this.Tj = option.type
		}
	}
</script>

<style>

</style>
