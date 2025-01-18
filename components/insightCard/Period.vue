<template>
	<view class="card">
		<view class="card-title">
			<view class="card-title-left">
				<view class="card-title-left-icon"></view>
				<view class="card-title-left-content">
					<view>Period</view>
					<view>Last 7 Day</view>
				</view>
			</view>
			<view class="card-title-right"></view>
		</view>
		<view class="card-content">
			<view class="card-content-title">
				<view>Day of Cycle</view>
				<view>7/9hr</view>
			</view>
			<view class="card-content-content">
				<uv-line-progress :percentage="30" :showText="false" activeColor="#FFB4B4"></uv-line-progress>
				<view class="yuanhuanBox">
					<view class="yuanItem" v-for="item in days">
						<view class="yuan"></view>
						<view class="text">
							{{ item }}
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				days: ['S', 'M', 'T', 'W', 'T', 'F', 'S']
			}
		}
	}
</script>

<style lang="scss" scoped>
	.card {
		background-color: #fff;
		border-radius: 24rpx;
		border: 1px solid #ECEFF3;
		padding: 18rpx;

		&-content {
			border-radius: 32rpx;
			padding: 32rpx;
			background-color: #f9f9f9;

			&-title {
				display: flex;
				align-items: center;
				justify-content: space-between;
				font-size: 28rpx;
				color: #0D0D12;
				margin-bottom: 32rpx;
			}
		}

		&-title {
			display: flex;
			justify-content: space-between;
			align-items: center;
			margin-bottom: 12rpx;


			&-right {
				width: 78rpx;
				height: 78rpx;
				background-color: #f9f9f9;
				border-radius: 100%;
				flex-shrink: 0;
			}

			&-left {
				display: flex;
				align-items: center;

				&-icon {
					width: 88rpx;
					height: 88rpx;
					background-color: #f9f9f9;
					border-radius: 100%;
					flex-shrink: 0;
					margin-right: 8rpx;
				}

				&-content {
					view:first-child {
						font-size: 32rpx;
						font-weight: bold;
						margin-bottom: 4rpx;
					}

					view:last-child {
						font-size: 24rpx;
						color: #818898;
					}
				}
			}
		}
	}

	.yuanhuanBox {
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		grid-gap: 8rpx;
		margin-top: 32rpx;

		.yuanItem {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			position: relative;
			.yuan {
				width: 70rpx;
				height: 70rpx;
				border-radius: 100%;
				border: 4rpx solid #fff;
				background-color: #FFB4B4;
			}
			.text {
				margin-top: 32rpx;
			}
		}
	}
	
	
</style>