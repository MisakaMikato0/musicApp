<template>
	<view>
		<view style="text-align: center;">欢迎使用Music</view>
		<view>
			<form @submit="formSubmit">
					<view class="uni-form-item">
							<view class="title">电话:</view>
							<input class="uni-input" name="input" placeholder="这是一个输入框" />
					</view>
					<view class="uni-form-item">
							<view class="title">密码:</view>
							<input class="uni-input" name="input" placeholder="这是一个输入框" />
					</view>
			</form>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss">
	.uni-form-item{
		display: flex;
		.title {
			padding: 0 20rpx;
		}
		.uni-input {
			border: 1px solid black; border-radius: 10px;
		}
	}
</style>
