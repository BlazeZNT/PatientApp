<template>
	<view class="card">
		<view class="titleBox">
			<view class="title" v-html="title">
			</view>
			<view class="icon">
				
			</view>
		</view>
		<view class="content">
			<view class="data">{{ data }}</view>
			<view class="unit">{{ unit }}</view>
		</view>
	</view>
</template>

<script setup>
	const props = defineProps({
		title: String,
		data: String,
		unit: String,
		icon: String
	})
</script>

<style lang="scss" scoped>
	.card {
		background-color: #fff;
		border-radius: 24rpx;
		border: 1px solid #ECEFF3;
		padding: 18rpx;
		.content {
			display: flex;
			align-items: flex-end;
			.data {
				font-size: 40rpx;
				margin-right: 10rpx;
			}
			
			.unit {
				font-size: 28rpx;
				color: #818898;
			}
		}
		.titleBox {
			display: flex;
			justify-content: space-between;
			margin-bottom: 20rpx;
			// align-items: center;
			.title {
				font-weight: bold;
				font-size: 32rpx;
				margin-right: 20rpx;
			}
			.icon {
				width: 80rpx;
				height: 80rpx;
				background-color: #F9F9F9;
				border-radius: 100%;
				flex-shrink: 0;
			}
		}
	}
</style>