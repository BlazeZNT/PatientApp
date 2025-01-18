<template>
	<view class="page">
		<uv-navbar title="Sleep Quality" placeholder @leftClick="leftClick"></uv-navbar>
		<view class="tabs">
			<view class="tabs-item" :class="item == activeTab ? 'active' : ''" @click="activeTab = item"
				v-for="item in tabs" :key="item">{{ item }}</view>
		</view>
		<view class="chartBox">
			<view style="width: 100%; height:150rpx"><l-echart ref="chart"></l-echart></view>
			<view class="tips">
				<view>00:00</view>
				<view>24:00</view>
			</view>
		</view>
		<view class="cardBox">
			<DataCard title="Total<br> Hours" data="7.5" unit="hours"></DataCard>
			<DataCard title="Time in<br> Bed" data="5,5" unit="hours"></DataCard>
			<DataCard title="Restful-<br>ness" data="82" unit="%"></DataCard>
			<DataCard title="Resting Heart Rate" data="6" unit="hours"></DataCard>
		</view>

		<view class="box">
			<view class="label">
				Sleep Overview
			</view>
			<view class="sublabel">
				Today, Wednesday 7 Aug 2024
			</view>
		</view>

		<scroll-view class="scroll-view_H" scroll-x="true" scroll-left="120">
			<view class="scroll-view-item_H" v-for="item in days" :key="item">
				<view class="icon"></view>
				<view class="text">{{ item }}</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	import * as echarts from 'echarts'
	import DataCard from '@/components/DataCard.vue'

	export default {
		components: {
			DataCard
		},
		data() {
			return {
				activeTab: 'Day',
				tabs: ['Day', 'Week', 'Month', 'Year'],
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
	.page {
		padding: 32rpx;

		.tabs {
			display: grid;
			padding: 4rpx;
			grid-template-columns: repeat(4, 1fr);
			grid-gap: 8rpx;

			.tabs-item {
				width: 100%;
				padding: 16rpx 0;
				display: flex;
				justify-content: center;
				align-items: center;
				color: #A4ACB9;

				&.active {
					color: #000;
					font-weight: bold;
					background-color: #fff;
					border-radius: 100rpx;
					box-shadow: 0 0 20rpx 0rpx rgba(0, 0, 0, 0.1);
				}
			}
		}
	}

	.chartBox {
		.tips {
			display: flex;
			justify-content: space-between;
			font-size: 24rpx;
			color: #818898;
		}
	}

	.cardBox {
		margin-top: 32rpx;
		display: grid;
		grid-template-columns: repeat(2, 1fr);
		grid-gap: 32rpx;
	}

	.box {
		margin-top: 32rpx;

		.label {
			font-weight: bold;
			font-size: 32rpx;
		}

		.sublabel {
			display: flex;
			justify-content: space-between;
			font-size: 24rpx;
			color: #818898;
			margin-top: 20rpx;
		}
	}

	.scroll-view_H {
		white-space: nowrap;
		width: 100%;
		margin-top: 20rpx;

		.scroll-view-item_H {
			width: auto !important;
			// display: flex;
			display: inline-block;
			justify-content: center;
			flex-direction: column;
			align-items: center;
			margin-right: 32rpx;
			.icon {
				width: 80rpx;
				height: 80rpx;
				border-radius: 100%;
				background-color: #818898;
			}
			.text {
				width: 100%;
				text-align: center;
				margin-top: 20rpx;
			}
		}
	}
</style>