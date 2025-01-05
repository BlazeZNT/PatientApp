<template>
	<view class="card">
		<view class="titleBox">
			<view class="numBox">1</view>
			<view class="title">
				<view class="icon">
					<image src="/static/icon/heart.png" mode=""></image>
				</view>
				<text>Spirometry</text>
			</view>
			<view class="date">12 March 2021</view>
		</view>
		<view class="contentBox">
			<view class="dataItem" v-for="item in 3" :class="'color' + item" :key="item">
				<view class="dateText1">
					FEV6
				</view>
				<view class="dateText2">
					102%
				</view>
			</view>
		</view>
		<view class="footer">
			Quality: <b>Grade A</b>
		</view>
	</view>
</template>

<script>
</script>

<style lang="scss" scoped>
	.card {
		width: 100%;
		height: 346rpx;
		background: #FFFFFF;
		border-radius: 20rpx 20rpx 20rpx 20rpx;
		border: 2rpx solid #EEEEEE;
		padding: 26rpx 32rpx;
		overflow: hidden;
		position: relative;
		.footer {
			width: 100%;
			height: 58rpx;
			margin-top: 30rpx;
			background: #FAFAFA;
			border-radius: 0rpx 0rpx 20rpx 20rpx;
			border: 0rpx solid rgba(238,238,238,0.5);
			font-weight: 400;
			font-size: 24rpx;
			color: #2B3348;
			display: flex;
			justify-content: center;
			align-items: center;
			position: absolute;
			bottom: 0;
			left: 0;
			b {
				font-weight: 700;
			}
		}
		.contentBox {
			display: flex;
			justify-content: space-between;
			margin-top: 36rpx;

			.dataItem {
				width: 186rpx;
				height: 158rpx;
				background: #F1FCFF;
				border-radius: 48rpx 48rpx 48rpx 48rpx;
				display: flex;
				flex-direction: column;
				justify-content: center;
				align-items: center;
				
				&.color1 {
					background-color: #F1FCFF;
				}
				&.color2 {
					background-color: #FFFCF1;
				}
				&.color3 {
					background-color: #FDF9FF;
				}

				.dateText1 {
					font-weight: 400;
					font-size: 28rpx;
					color: #000000;
				}

				.dateText2 {
					font-weight: 800;
					font-size: 32rpx;
					color: #0034EE;
					margin-top: 8rpx;
				}
			}
		}

		.titleBox {
			display: flex;
			align-items: center;

			.numBox {
				width: 64rpx;
				height: 40rpx;
				background: #0034EE;
				box-shadow: 0rpx 4rpx 12rpx 0rpx rgba(32, 76, 178, 0.3);
				border-radius: 86rpx 86rpx 86rpx 86rpx;
				font-size: 26rpx;
				color: #FFFFFF;
				display: flex;
				justify-content: center;
				align-items: center;
				margin-right: 22rpx;
			}

			.title {
				display: flex;
				align-items: center;
				font-weight: 600;
				font-size: 32rpx;
				color: #000000;
				flex: 1;

				.icon {
					width: 38rpx;
					height: 38rpx;
					margin-right: 8rpx;
				}
			}

			.date {
				font-weight: 600;
				font-size: 26rpx;
				color: rgba(26, 26, 26, 0.7);
			}
		}
	}
</style>