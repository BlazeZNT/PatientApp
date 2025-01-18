<template>
	<view class="page">
		<uv-navbar title="Period" placeholder @leftClick="leftClick"></uv-navbar>
		<lxCalendar :retract="false" />
		<view class="card">
			<view class="title">
				Cycle Statistics
			</view>
			<view class="chartBox">
				<view style="width: 100%; height:300rpx"><l-echart ref="chart1"></l-echart></view>
				<view style="width: 100%; height:300rpx"><l-echart ref="chart2"></l-echart></view>
				<view style="width: 100%; height:300rpx"><l-echart ref="chart3"></l-echart></view>
			</view>
		</view>
	</view>
</template>

<script>
	import lxCalendar from '../../components/lx-calendar/lx-calendar.vue'
	import * as echarts from 'echarts'

	export default {
		components: {
			lxCalendar
		},
		mounted() {
			this.$refs.chart1.init(echarts, chart => {
				chart.setOption(this.options)
			})
			this.$refs.chart2.init(echarts, chart => {
				chart.setOption(this.options)
			})
			this.$refs.chart3.init(echarts, chart => {
				chart.setOption(this.options)
			})
		},
		data() {
			var trafficWay = [{
					name: "",
					value: 20,
				},
				{
					name: "",
					value: 10,
				},
				{
					name: "",
					value: 30,
				},
			];

			var data = [];
			var color = [
				"#00ffff",
				"#00cfff",
				"#006ced",
				"#ffe000",
				"#ffa800",
				"#ff5b00",
				"#ff3000",
			];
			for (var i = 0; i < trafficWay.length; i++) {
				data.push({
					value: trafficWay[i].value,
					name: trafficWay[i].name,
					itemStyle: {
						normal: {
							borderWidth: 8,
							borderColor: color[i],
						},
					},
				}, {
					value: 2,
					name: "",
					itemStyle: {
						normal: {
							label: {
								show: false,
							},
							labelLine: {
								show: false,
							},
							color: "rgba(0, 0, 0, 0)",
							borderColor: "rgba(0, 0, 0, 0)",
							borderWidth: 0,
						},
					},
				});
			}
			let seriesOption = [{
				name: "",
				type: "pie",
				clockWise: false,
				radius: [40, 40],
				hoverAnimation: false,
				itemStyle: {
					normal: {
						label: {
							show: false,
							position: "outside",
							color: "#ddd",
							formatter: function(params) {
								var percent = 0;
								var total = 0;
								for (var i = 0; i < trafficWay.length; i++) {
									total += trafficWay[i].value;
								}
								percent = ((params.value / total) * 100).toFixed(0);
								if (params.name !== "") {
									return params.name + "\n" + "\n" + "占百分比：" + percent + "%";
								} else {
									return "";
								}
							},
						},
						labelLine: {
							length: 30,
							length2: 100,
							show: true,
							color: "#00ffff",
						},
					},
				},
				data: data
			}]
			return {

				options: {
					// backgroundColor: "#0A2E5D",
					color: color,
					title: {
						text: "Period Length",
						bottom: "0",
						textAlign: "center",
						left: "49%",
						textStyle: {
							color: "#000",
							fontSize: 14,
							fontWeight: "400",
						},
					},
					tooltip: {
						show: false,
					},
					legend: {
						show: false,
						icon: "circle",
						orient: "horizontal",
						data: [],
						right: 250,
						bottom: 100,
						align: "right",
						textStyle: {
							color: "#fff",
						},
						itemGap: 20,
					},
					toolbox: {
						show: false,
					},
					series: seriesOption,
				},

			}
		}
	}
</script>

<style lang="scss" scoped>
	.page {
		padding: 32rpx;
	}

	.card {
		border-radius: 32rpx;
		padding: 32rpx;
		border: 1px solid #ECEFF3;
		margin-top: 32rpx;

		.title {
			font-size: 32rpx;
			font-weight: bold;
		}
		
		.chartBox {
			display: grid;
			grid-template-columns: repeat(3, 1fr);
		}
	}
</style>