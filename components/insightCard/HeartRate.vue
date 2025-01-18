<template>
	<view class="card">
		<view class="card-title">
			<view class="card-title-left">
				<view class="card-title-left-icon"></view>
				<view class="card-title-left-content">
					<view>Heart Rate</view>
					<view>Last 7 Day</view>
				</view>
			</view>
			<view class="card-title-right"></view>
		</view>
		<view class="card-content">
			<view class="card-content-title">
				<view>Today</view>
				<view>72-90Bpm</view>
			</view>
			<view class="card-content-content">
				<view style="width: 100%; height:100rpx"><l-echart ref="chart"></l-echart></view>
				<view class="tip">
					<view>00:00</view>
					<view>24:00</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import * as echarts from 'echarts'

	export default {
		data() {
			return {
				days: ['S', 'M', 'T', 'W', 'T', 'F', 'S']
			}
		},
		mounted() {
			this.$refs.chart.init(echarts, chart => {
				chart.setOption({
					title: {
						show: false
					},
					tooltip: {
						show: false,
						trigger: "axis",
						axisPointer: {
							type: "shadow",
						},
					},
					grid: {
						top: "0",
						right: "0",
						left: "0",
						bottom: 6,
					},
					xAxis: [{
						min: 0,
						max: 24,
						type: "category",
						data: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19,
							20, 21, 22, 23, 24
						],
						axisLine: {
							show: false
						},
						axisTick: {
							show: true,
							alignWithLabel: true,
							lineStyle: {
								color: '#ECEFF3'
							}
						},
						splitLine: {
							show: false,
						},
						axisLabel: {
							show: false
						}
					}, ],
					yAxis: {
						show: false,
					},
					series: [{
						type: "bar",
						data: [
							72,
							82,
							92,
							60,
							50,
							98,
							76,
							69,
							72,
							82,
							92,
							60,
							50,
							98,
							76,
							69,
							72,
							82,
							92,
							60,
							50,
							98,
							76,
							69
						],
						barWidth: "4px",
						itemStyle: {
							normal: {
								color: function(params) {
									// let color = ''
									if(params.value >= 60 ) {
										return '#FFB4B4'
									}else {
										return '#B1DE35'
									}
								},
								// color: '#FFB4B4',
								barBorderRadius: [30, 30, 30, 30],
							},
						},
					}, ],
				});
			});
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

			.tip {
				display: flex;
				justify-content: space-between;
				font-size: 24rpx;
				margin-top: 4rpx;
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
</style>