<template>
	<view class="card">
		<view class="card-title">
			<view class="card-title-left">
				<view class="card-title-left-icon"></view>
				<view class="card-title-left-content">
					<view>Sleep Quality</view>
					<view>Last 7 Day</view>
				</view>
			</view>
			<view class="card-title-right"></view>
		</view>
		<view class="card-content">
			<view class="card-content-title">
				<view>Today</view>
				<view>6,5/8hr</view>
			</view>
			<view class="card-content-content">
				<view style="width: 100%; height:150rpx"><l-echart ref="chart"></l-echart></view>
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
			const colorList = [
				'#C3EAFF',
				'#2F2F96',
				new echarts.graphic.LinearGradient(
					0,
					0,
					0,
					1, 
					[{
							offset: 0,
							color: '#52F5D7', // 0% 处的颜色
						},
						{
							offset: 1,
							color: '#35C8F4', // 100% 处的颜色
						},
					],
					false
				)
			];
			const data = [
				[0, 24, 3, 'A'],
				[10, 11, 4, 'B'],
				[13, 14, 4, 'C'],
				[18, 19, 6, 'C'],
			].map(function(item, index) {
				let color = item[3] == 'C' ? colorList[2] : item[3] == 'B' ? colorList[1] : colorList[0]
				return {
					value: item,
					itemStyle: {
						color: color
					}
				};
			});
			this.$refs.chart.init(echarts, chart => {
				chart.setOption({
					title: {
						show: false
					},
					grid: {
						top: 10,
						bottom: 3,
						left: 10,
						right: 10
					},
					tooltip: {},
					xAxis: {
						min: 0,
						max: 24,
						splitNumber: 24,
						position: 'bottom',
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
					},
					yAxis: {
						show: false,
						axisLine: {
							show: false
						},
						axisTick: {
							show: false
						},
						splitLine: {
							show: false
						}
					},
					series: [{
						type: 'custom',
						renderItem: function(params, api) {
							var yValue = api.value(2);
							var start = api.coord([api.value(0), yValue]);
							var size = api.size([api.value(1) - api.value(0), yValue]);
							var style = api.style();
							return {
								type: 'rect',
								shape: {
									x: start[0],
									y: start[1],
									width: size[0],
									height: size[1]
								},
								style: style
							};
						},
						label: {
							show: false,
							position: 'top'
						},
						dimensions: ['from', 'to', 'profit'],
						encode: {
							x: [0, 1],
							y: 2,
							tooltip: [0, 1, 2],
							itemName: 3
						},
						data: data
					}]
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