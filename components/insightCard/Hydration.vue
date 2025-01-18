<template>
	<view class="card">
		<view class="card-title">
			<view class="card-title-left">
				<view class="card-title-left-icon"></view>
				<view class="card-title-left-content">
					<view>Hydration</view>
					<view>Last 7 Day</view>
				</view>
			</view>
			<view class="card-title-right"></view>
		</view>
		<view class="card-content">
			<view class="card-content-title">
				<view>Today</view>
				<view>1,203/1,500/cal</view>
			</view>
			<view class="card-content-content">
				<uv-line-progress :percentage="30" :showText="false" activeColor="#0A7DFF"></uv-line-progress>
				<view class="yuanhuanBox">
					<view class="yuanItem" v-for="item in days">
						<l-circle :current="20" size="40" :strokeWidth="4" :trailWidth="4" trailColor="#ffffff"
							strokeColor="#0A7DFF" :percent="50">
						</l-circle>
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

			.text {
				margin-top: 32rpx;
			}
		}
	}
</style>